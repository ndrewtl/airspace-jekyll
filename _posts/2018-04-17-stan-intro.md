---
layout: post
title: Intro to Stan
subtitle: Getting started with Bayesian modelling in Stan
date: 2018-04-17 08:00:00
author: Maxwell Farrell & Isla Myers-Smith
meta: "Tutorials"
tags: modelling advanced
---

<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheader_stan.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#intro"> 1. Learn about `Stan`</a>

#### <a href="#data"> 2. Prepare a dataset for modelling</a>

#### <a href="#stan"> 3. Write a programme in `Stan`</a>

#### <a href="#run"> 4. Run a `Stan` programme</a>

#### <a href="#priors"> 5. Specify priors in `Stan`</a>

#### <a href="#priors"> 6. Assess convergence diagnostics</a>


#### All the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-Stan-intro" target="_blank">this repository</a>. Click on `Clone/Download/Download ZIP` and unzip the folder, or clone the repository to your own GitHub account.


### 1. Learn about `Stan`

<a name="intro"></a>

__Bayesian modelling like any statistical modelling can require work to design the appropriate model for your research question and then to develope that model so that it meets the assumptions of your data and runs. You can check out the Coding Club tutorial on <a href="https://ourcodingclub.github.io/2018/04/06/model-design.html" target="_blank"> how to design a model</a>, and <a href="https://ourcodingclub.github.io/2018/01/22/mcmcglmm.html" target="_blank">Bayesian Modelling in `MCMCglmm`</a> for key background information on model design and Bayesian statistics.__

__Statistical models can be fit in a variety of packages in `R` or other statistical languages. But sometimes the perfect model that you can design conceptually is very hard or impossible to implement in a package or programme that restricts the distributions and complexity that you can use. This is when you may want to move to a statistical programming language such as <a href="http://mc-stan.org/" target="_blanl">`Stan`</a>.__

`Stan` is a new-ish language that offers a more comprehensive approach to learning and implementing Bayesian models that can fit complex data structures. A goal of the `Stan` development team is to make Bayesian modelling more accessible with clear syntax, a better sampler (sampling here refers to drawing samples out of the Bayesian posterior distribution), and integration with many platforms and including `R`, `RStudio`, `ggplot2`, and `Shiny`.

In this introductory tutorial we'll go through the iterative process of model building starting with a linear model. In our advanced `Stan` tutorial we will explore more complex model structures.

First, before building a model you need to define your question and get to know your data. Explore them, plot them, calculate some summary statistics.

Once you have a sense of your data and what question you want to answer with your statistical model, you can begin the iterative process of building a Bayesian model:

1. Design your model.
2. Choose priors (Informative? Not? Do you have external data you could turn into a prior?)
3. Sample the posterior distribution.
4. Inspect model convergence (traceplots, rhats, and for Stan no divergent transitions - we will go through these later in the tutorial)
6. Critically assess the model using posterior predictions and checking how they compare to your data!
7. Repeat...

It's also good practice to simulate data to make sure your model is doing what you think it's doing, as a further way to test your model!

<a name="data"></a>

### 2. Data

__First, let's find a dataset where we can fit a simple linear model. <a href="https://nsidc.org/" target="_blank">The National Snow and Ice Data Center</a> provides loads of public data that you can download and explore. One of the most prominent climate change impacts on planet earth is the decline in annual sea ice extent in the Northern Hemisphere. Let's explore how sea ice extent is changing over time using a linear model in Stan.__

Set your working directory to the folder where you've saved the data by either clicking on `Session/Set working directory/Choose directory` or running the code `setwd("your-file-path")` with your own filepath inside. Now, let's load the data:

```r
# Adding stringsAsFactors = F means that numeric variables won't be
# read in as factors/categorical variables
seaice <- read.csv("seaice.csv", stringsAsFactors = F)
```

Let's have a look at the data:

```r
head(seaice)
```

If for some reason the column names are not read in properly, you can change column names using:

```r
colnames(seaice) <- c("year", "extent_north", "extent_south")
```

__What research question can we ask with these data? How about the following:__

### _Research Question:_ Is sea ice extent declining in the Northern Hemisphere over time?

To explore the answer to that question, first we can make a figure.

```r
(extent_north ~ year, pch = 20, data = seaice)
```

<center> <img src="{{ site.baseurl }}/img/sea_ice1.png" alt="Img" style="width: 600px;"/> </center>
<center>Figure 1. Change in sea ice extent in the Northern Hemisphere over time.</center>

Now, let's run a general linear model using `lm()`.

```r
lm1 <- lm(extent_north ~ year, data = seaice)
summary(lm1)
```

We can add that model fit to our plot:

```r
abline(lm1, col = 2, lty = 2, lw = 3)
```

<center> <img src="{{ site.baseurl }}/img/sea_ice2.png" alt="Img" style="width: 600px;"/> </center>
<center>Figure 2. Change in sea ice extent in the Northern Hemisphere over time (plus linear model fit).</center>

__Let's remember the equation for a linear model:__

y = α + β∗x + error

In `Stan` you need to specify the equation that you are trying to model, so thinking about that model equation is key!

We have the answer to our question perhaps, but the point of this tutorial is to explore using the programming language `Stan`, so now let's try writing the same model in Stan.

### Preparing the data

Let's rename the variables and index the years from 1 to 39. One critical thing about Bayesian models is that you have to describe the variation in your data with informative distributions. Thus, you want to make sure that your data do conform to those distributions and that they will work with your model. In this case, we really want to know is sea ice changing from the start of our dataset to the end of our dataset, not specifically the years 1979 to 2017 which are really far from the year 0. We don't need our model to estimate what sea ice was like in the year 500, or 600, just over the duration of our dataset. So we set up our year data to index from 1 to 30 years.

```r
x <- I(seaice$year - 1978)
y <- seaice$extent_north
N <- length(seaice$year)
```

We can re-run that linear model with our new data.

```r
lm1 <- lm(y ~ x)
summary(lm1)
```

We can also extract some of the key summary statistics from our simple model, so that we can compare them with the outputs of the `Stan` models later.

```r
lm_alpha <- summary(lm1)$coeff[1]  # the intercept
lm_beta <- summary(lm1)$coeff[2]  # the slope
lm_sigma <- sigma(lm1)  # the residual error
```

__Now let's turn that into a dataframe for inputting into a `Stan` model. Data passed to Stan needs to be a list of named objects. The names given here need to match the variable names used in the models (see the model code below).__

```r
stan_data <- list(N = N, x = x, y = y)
```

#### Libraries

Please make sure the following libraries are installed (these are the libraries for this and the next `Stan` tutorial). `rstan` is the most important, and requires a little extra if you dont have a C++ compiler.

__You can find detailed instructions <a href="https://github.com/stan-dev/rstan/wiki/RStan-Getting-Started" target="_blank">here</a>.__

```r
library(rstan)
library(gdata)
library(bayesplot)
library(rstanarm)
library(shinystan)
library(loo)
```

<a name="stan"></a>

### 3. Our first `Stan` program

__We're going to start by writing a linear model in the language `Stan`. This can be written in your R script, or saved seprately as a `.stan` file and called into `R`.__

__A `Stan` program has three required "blocks":__

1. **"data"** block: where you declare the data types, their dimensions, any restrictions (i.e. upper = or lower = , which act as checks for `Stan`), and their names. Any names you give to your `Stan` program will also be the names used in other blocks.

2. **"parameters"** block: This is where you indicate the parameters you want to model, their dimensions, restrictions, and name. For a linear regression, we will want to model the intercept, any slopes, and the standard deviation of the errors around the regression line.

3. **"model"** block: This is where you include any sampling statements, including the "likelihood" (model) you are using. The model block is where you indicate any prior distributions you want to include for your parameters. If no prior is defined, `Stan` uses default priors of `uniform(-infinity, +infinity)`. You can restrict priors using upper or lower when declaring the parameters (i.e. `lower = 0`> to make sure a parameter is positive).

__Sampling is indicated by the `~` symbol, and `Stan` already includes many common distributions as vectorized functions. You can check out <a href="http://mc-stan.org/users/documentation/" target="_blank">the manual</a> for a comprehensive list and more information on the optional blocks you could include in your `Stan` model.__

There are also four optional blocks:

* **"functions"**
* **"transformed data"**
* **"transformed parameters"**
* **"generated quantities"**

Comments are indicated by `//` in Stan. The `write("model code", "file_name")` bit allows us to write the Stan model in our R script and output the file to the working directory (or you can set a different file path).

```r
write("// Stan model for simple linear regression

data {
 int < lower = 1 > N; // Sample size
 vector[N] x; // Predictor
 vector[N] y; // Outcome
}

parameters {
 real alpha; // Intercept
 real beta; // Slope (regression coefficients)
 real < lower = 0 > sigma; // Error SD
}

model {
 y ~ normal(alpha + x * beta , sigma);
}

generated quantities {
} // The posterior predictive distribution",

"stan_model1.stan")
```

First, we should check our `Stan` model to make sure we wrote a file.

```r
stanc("stan_model1.stan")
```

Now let's save that file path.

```r
stan_model1 <- "scripts/users/imyerssmith/CC-Stan-Part-1/stan_model1.stan"
```

__Here we are implicitly using `uniform(-infinity, +infinity)` priors for our parameters. These are also known as "flat" priors or "non-informative" priors.__

<a name="run"></a>

### 4. Running our `Stan` model

__Stan programs are complied to `C++` before being used. This means that the C++ code needs to be run before R can use the model. For this you must have a `C++` compiler installed (see <a href="https://github.com/stan-dev/rstan/wiki/RStan-Getting-Started" target="_blank">this wiki if you don't have one already</a>). You can use your model many times per session once you compile it, but you must re-compile when you start a new `R` session. There are many `C++` compilers and they are often different across systems. If your model spits out a bunch of errors (unintelligible junk), don't worry. As long as your model can be used with the `stan()` function, it compiled correctly. If we want to use a previously written `.stan` file, we use the `file` argument in the `stan_model()` function.__

We fit our model by using the `stan()` function, and providing it with the model, the data, and indicating the number of iterations for warmup (these iterations won't be used for the posterior distribution later, as they were just the model "warming up"), the total number of iterations, how many chains we want to run, the number of cores we want to use (`Stan` is set up for parallelization), which indicates how many chains are run simultaneously (i.e., if you computer has four cores, you can run one chain on each, making for four at the same time), and the thinning, which is how often we want to store our post-warmup iterations. "thin = 1" will keep every iteration, "thin = 2" will keep every second, etc...

`Stan` automatically uses half of the iterations as warm-up, if the `warmup =` argument is not specified.

```r
fit <- stan(file = stan_model1, data = stan_data, warmup = 500, iter = 1000, chains = 4, cores = 2, thin = 1)
```

### Accessing the contents of a `stanfit` object

__Results from `stan()` are saved as a `stanfit` object (S4 class). You can find more details in the `Stan` <a href=" https://cran.r-project.org/web/packages/rstan/vignettes/stanfit-objects.html
" target="_blank"> https://cran.r-project.org/web/packages/rstan/vignettes/stanfit-objects.html
vignette </a>.__

__We can get summary statistics for parameter estimates, and sampler diagnostics by executing the name of the object:__

```r
fit
```

<center> <img src="{{ site.baseurl }}/img/stan_summary.png" alt="Img" style="width: 600px;"/> </center>

__What does the model output show you?  How do you know your model has converged?  Can you see that text indicating that your C++ compiler has run?__

__From this output we can quickly assess model convergence by looking at the `Rhat` values for each parameter. When these are at or near 1, the chains have converged. There are many other diagnostics, but this is an important one for Stan.__

We can also look at the full posterior of our parameters by extracting them from the model object. There are many ways to view the posterior.

```r
posterior <- extract(fit)
str(posterior)
```

`extract()` puts the posterior estimates for each parameter into a list.

Let's compare to our previous estimate with "lm":

```r
plot(y ~ x, pch = 20)

abline(lm1, col = 2, lty = 2, lw = 3)
abline( mean(posterior$alpha), mean(posterior$beta), col = 6, lw = 2)
```

<center> <img src="{{ site.baseurl }}/img/sea_ice3.png" alt="Img" style="width: 400px;"/> <img src="{{ site.baseurl }}/img/sea_ice4.png" alt="Img" style="width: 400px;"/></center>
<center>Figure 3. Change in sea ice extent in the Northern Hemisphere over time (comparing a `Stan` linear model fit and a general `lm` fit).</center>

The result is identical to the `lm` output. This is because we are using a simple model, and have put non-informative priors on our parameters.

One way to visualize the variability in our estimation of the regression line is to plot multiple estimates from the posterior.

```r
for (i in 1:500) {
 abline(posterior$alpha[i], posterior$beta[i], col = "gray", lty = 1)
}
```

```r
plot(y ~ x, pch = 20)

for (i in 1:500) {
 abline(posterior$alpha[i], posterior$beta[i], col = "gray", lty = 1)
}

abline(mean(posterior$alpha), mean(posterior$beta), col = 6, lw = 2)
```

<center> <img src="{{ site.baseurl }}/img/sea_ice5.png" alt="Img" style="width: 600px;"/> </center>
<center>Figure 4. Change in sea ice extent in the Northern Hemisphere over time (`Stan` linear model fits).</center>

<a name="priors"></a>

### 5. Changing our priors

__Let's try again, but now with more informative priors for the relationship between sea ice and time. We're going to use normal priors with small standard deviations. If we were to use normal priors with very large standard deviations (say 1000, or 10,000), they would act very similarly to uniform priors.__

```r

write("// Stan model for simple linear regression

data {
 int < lower = 1 > N; // Sample size
 vector[N] x; // Predictor
 vector[N] y; // Outcome
}

parameters {
 real alpha; // Intercept
 real beta; // Slope (regression coefficients)
 real < lower = 0 > sigma; // Error SD
}

model {
 alpha ~ normal(10, 0.1);
 beta ~ normal(1, 0.1);
 y ~ normal(alpha + x * beta , sigma);
}

generated quantities {}",

"stan_model2.stan")

stan_model2 <- "scripts/users/imyerssmith/CC-Stan-Part-1/stan_model2.stan"
```

__We'll fit this model and compare it to the mean estimate using the uniform priors.__

```r
fit2 <- stan(stan_model2, data = stan_data, warmup = 500, iter = 1000, chains = 4, cores = 2, thin = 1)

posterior2 <- extract(fit2)

plot(y ~ x, pch = 20)

abline(alpha, beta, col = 4, lty = 2, lw = 2)
abline(mean(posterior2$alpha), mean(posterior2$beta), col = 3, lw = 2)
abline(mean(posterior$alpha), mean(posterior$beta), col = 36, lw = 3)
```

<center> <img src="{{ site.baseurl }}/img/stan_fits.png" alt="Img" style="width: 600px;"/> </center>
<center>Figure 5. Change in sea ice extent in the Northern Hemisphere over time (`Stan` linear model fits).</center>

__So what happened to the posterior predictions (your modelled relationship)? Does the model fit the data better or not? Why did the model fit change? What did we actually change about our model by making very narrow prior distributions? Try changing the priors to some different numbers yourself and see what happens! This is a common issue in Bayesian modelling, if your prior distributions are very narrow and yet don't fit your understanding of the system or the distribution of your data, you could run models that do not meaningfully explain variation in your data. However, that isn't to say that you shouldn't choose somewhat informative priors, you do want to use previous analyses and understanding of your study system inform your model priors and design. You just need to think carefully about each modelling decision you make!__

<a name="convergence"></a>

### 6. Convergence Diagnostics

__Before we go on, we should check again the `Rhat` values, the effective sample size (`n_eff`), and the traceplots of our model parameters to make sure the model has converged and is reliable. To find out more about what these model checks are doing, you can check out the tutorial on <a href="https://ourcodingclub.github.io/2018/01/22/mcmcglmm.html" target="_blank">Bayesian statistics using `MCMCglmm`</a>.__

`n_eff` is a crude measure of the effective sample size. You usually only need to worry is this number is less than 1/100th or 1/1000th of
your number of iterations.

	'Anything over an `n_eff` of 100 is usually "fine"' - Bob Carpenter

For traceplots, we can view them directly from the posterior:

```r
plot(posterior$alpha, type = "l")
plot(posterior$beta, type = "l")
plot(posterior$sigma, type = "l")
```

<center> <img src="{{ site.baseurl }}/img/sea_ice5.png" alt="Img" style="width: 600px;"/> </center>
<center>Figure 6. Trace plot for alpha, the intercept.</center>

For simpler models, convergence is usually not a problem unless you have a bug in your code, or run your sampler for too few iterations.


#### Poor convergence

Try running a model for only 50 iterations and check the traceplots.

```r
fit_bad <- stan(model1, data = stan_data, warmup = 25, iter = 50, chains = 4, cores = 2, thin = 1)
posterior_bad <- extract(fit_bad)
```

__This also has some "divergent transitions" after warmup, indicating a mis-specified model, or that the sampler that has failed to fully sample the posterior (or both!). Divergent transitions sound like some sort of teen fiction about <a href="https://en.wikipedia.org/wiki/Divergent_trilogy" target="_blank">a future distopia</a>, but actually it indicates problems with your model.__


```r
plot(posterior_bad$alpha, type = "l")
plot(posterior_bad$beta, type = "l")
plot(posterior_bad$sigma, type = "l")
```

<center> <img src="{{ site.baseurl }}/img/bad_stan_traces.png" alt="Img" style="width: 600px;"/> </center>
<center>Figure 7. Bad trace plot for alpha, the intercept.</center>


#### Parameter summaries

We can also get summaries of the parameters through the posterior directly. Let's also plot the non-Bayesian linear model values to make sure our model is doing what we think it is...

```r
par(mfrow = c(1,3))

plot(density(posterior$alpha), main = "Alpha")
abline(v = lm_alpha, col = 4, lty = 2)

plot(density(posterior$beta), main = "Beta")
abline(v = lm_beta, col = 4, lty = 2)

plot(density(posterior$sigma), main = "Sigma")
abline(v = lm_sigma, col = 4, lty = 2)
```

<center> <img src="{{ site.baseurl }}/img/stan_panel.png" alt="Img" style="width: 900px;"/> </center>
<center>Figure 8. Density plot distributions from the `Stan` model fit compared with the estimates from the general `lm` fit.</center>

From the posterior we can directly calculate the probability of any parameter being over or under a certain value of interest.

**Probablility that beta is >0:**

```r
sum(posterior$beta>0)/length(posterior$beta)
```

**Probablility that beta is >0.2:**

```r
sum(posterior$beta>0.2)/length(posterior$beta)
```

#### Diagnostic plots in `rstan`

While we can work with the posterior directly, `rstan` has a lot of useful functions built-in.

```r
traceplot(fit)
```

<center> <img src="{{ site.baseurl }}/img/stan_chains.png" alt="Img" style="width: 900px;"/> </center>
<center>Figure 9. Trace plots of the different chains of the `Stan` model.</center>

This is a wrapper for the `stan_trace()` function, which is much better than our previous plot because it allows us to compare the chains.

We can also look at the posterior densities & histograms.

```r
stan_dens(fit)
stan_hist(fit)
```

<center> <img src="{{ site.baseurl }}/img/stan_density.png" alt="Img" style="width: 900px;"/> </center>
<center> <img src="{{ site.baseurl }}/img/stan_histogram.png" alt="Img" style="width: 900px;"/> </center>
<center>Figure 10. Density plots and histograms of the posteriors for the intercept, slope and residual variance from the `Stan` model.</center>

And we can generate plots which indicate the mean parameter estimates and any credible intervals we may be interested in. Note that the 95% credible intervals for the `beta` and `sigma` parameters are very small, thus you only see the dots.

```r
plot(fit, show_density = FALSE, ci_level = 0.5, outer_level = 0.95, fill_color = "salmon")
```

<center> <img src="{{ site.baseurl }}/img/stan_caterpillar.png" alt="Img" style="width: 900px;"/> </center>
<center>Figure 11. Parameter estimates from the `Stan` model.</center>

#### Posterior Predictive Checks

For prediction and as another form of model diagnostic, `Stan` can use random number generators to generate predicted values for each data point, at each iteration. For details, you can check out the <a href="https://cran.r-project.org/web/packages/bayesplot/index.html" target="_blank">vignettes</a>.


This way we can generate predictions that also represent the uncertainties in our model and our data generation process. We generate these using the Generated Quantities block. This block can be used to get any other information we want about the posterior, or make predictions for new data.

```stan

write("// Stan model for simple linear regression

data {
 int < lower = 1 > N; // Sample size
 vector[N] x; // Predictor
 vector[N] y; // Outcome
}

parameters {
 real alpha; // Intercept
 real beta; // Slope (regression coefficients)
 real < lower = 0 > sigma; // Error SD
}

model {
 y ~ normal(x * beta + alpha, sigma);
}

generated quantities {
 real y_rep[N];

 for (n in 1:N) {
 y_rep[n] = normal_rng(x[n] * beta + alpha, sigma);
 }

}",

"stan_model2_GQ.stan")

stan_model2_GQ <- "scripts/users/imyerssmith/CC-Stan-Part-1/stan_model2_GQ.stan"
```

Note that vectorization is not supported in the GQ (generated quantities) block, so we have to put it in a loop. But since this is compiled to `C++`, loops are actually quite fast and Stan only evaluates the GQ block once per iteration, so it won't add too much time to your sampling. Typically, the data generating functions will be the distributions you used in the model block but with an `_rng` suffix. (Double-check in the Stan manual to see which sampling statements have corresponding rng functions already coded up.)

```r
fit3 <- stan(stan_model2_GQ, data = stan_data, iter = 1000, chains = 4, cores = 2, thin = 1)
```

#### Extracting the `y_rep` values from posterior.

There are many options for dealing with `y_rep` values.

```r posterior
y_rep <- as.matrix(fit3, pars = "y_rep")
dim(y_rep)
```

Each row is an iteration (single posterior estimate) from the model.

We can use the `bayesplot` package to make some prettier looking plots. This package is a wrapper for many common `ggplot2` plots, and has a lot of built-in functions to work with posterior predictions.

Comparing density of `y` with densities of `y` over 200 posterior draws.

```r
ppc_dens_overlay(y, y_rep[1:200, ])
```

<center> <img src="{{ site.baseurl }}/img/bayes1.png" alt="Img" style="width: 500px;"/> </center>
<center>Figure 12. Comparing estimates across random posterior draws.</center>

Here we see data (dark blue) fit well with our posterior predictions.

We can also use this to compare estimates of summary statistics.

```r
ppc_stat(y = y, yrep = y_rep, stat = "mean")
```
<center> <img src="{{ site.baseurl }}/img/bayes2.png" alt="Img" style="width: 500px;"/> </center>
<center>Figure 13. Comparing estimates of summary statistics.</center>

We can change the function passed to the `stat` function, and even write our own!

We can investigate mean posterior prediction per datapoint vs the observed value for each datapoint (default line is 1:1)

```r
ppc_scatter_avg(y = y, yrep = y_rep)
```

<center> <img src="{{ site.baseurl }}/img/bayes2.png" alt="Img" style="width: 500px;"/> </center>
<center>Figure 14. Mean posterior prediction per datapoint vs the observed value for each datapoint.</center>


##### `bayesplot` options

Here is a list of currently available plots (`bayesplot 1.2`):

```r
available_ppc()
```

You can change the colour scheme in `bayesplot` too:

```r
color_scheme_view(c("blue", "gray", "green", "pink", "purple",
 "red","teal","yellow"))
```

<center> <img src="{{ site.baseurl }}/img/bayes_colours.png" alt="Img" style="width: 800px;"/> </center>

And you can even mix them:

```r
color_scheme_view("mix-blue-red")
```

You can set color schemes with:
```r
color_scheme_set("blue")
```


### Back to our research question


So now you have learned how to run a linear model in `Stan` and to check the model convergence. But what is the answer to our research question?

#### _Research Question:_ Is sea ice extent declining in the Northern Hemisphere over time?

What do your `Stan` model results indicate?

How would you write up these results? What is the key information to report from a Stan model? Effect sizes, credible intervals, sample sizes, what else?  Check out some Stan models in the ecological literature to see how those Bayesian models are reported.

#### Now as an added challenge, can you go back and test a second research question:

#### _Research Question:_ Is sea ice extent declining in the Southern Hemisphere over time?

Is the same pattern happening in the Antarctic as in the Arctic?  Fit a Stan model to find out!  

In the next Stan tutorial, we will build on the concept of a simple linear model in Stan to learn about more complex modelling structures including different distributions and random effects. And in a future tutorial, we will introduce the concept of a mixture model where two different distributions are modelled at the same time - a great way to deal with zero inflation in your proportion or count data!


### Stan References


__Stan is a run by a small, but dedicated group of developers. If you are new to Stan, you can join the mailing list. It's a great resource for understanding and diagnosing problems with Stan, and by posting problems you encounter you are helping yourself, and giving back to the community.__

<a href="http://mc-stan.org/" target="_blank">Stan website</a>

<a href="https://github.com/stan-dev/stan/releases/download/v2.14.0/stan-reference-2.14.0.pdf" target="_blank">Stan manual(v2.14)</a>

<a href="https://cran.r-project.org/web/packages/rstan/vignettes/rstan.html" target="_blank">Rstan vignette</a>

<a href="https://t.co/6d3omvBkrd" target="_blank">STANCON 2017 Intro Course Materials</a>

<a href="http://xcelab.net/rm/statistical-rethinking/" target="_blank">Statistical Rethinking by R. McElreath</a>

<a href="https://groups.google.com/forum/#!forum/stan-users" target="_blank">Stan mailing list</a>



<hr>
<hr>



<h3><a href="https://www.surveymonkey.co.uk/r/P39ZP2G" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>

<br>
<h3>&nbsp; You can contact us with any questions on <a href="mailto:ourcodingclub@gmail.com?Subject=Tutorial%20question" target = "_top">ourcodingclub@gmail.com</a></h3>
<br>
<h3>&nbsp; Related tutorials:</h3>

{% assign posts_thresh = 8 %}

<ul>
  {% assign related_post_count = 0 %}
  {% for post in site.posts %}
    {% if related_post_count == posts_thresh %}
      {% break %}
    {% endif %}
    {% for tag in post.tags %}
      {% if page.tags contains tag %}
        <li>
            <a href="{{ site.url }}{{ post.url }}">
	    &nbsp; - {{ post.title }}
            </a>
        </li>
        {% assign related_post_count = related_post_count | plus: 1 %}
        {% break %}
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>
<br>
<h3>&nbsp; Subscribe to our mailing list:</h3>
<div class="container">
	<div class="block">
        <!-- subscribe form start -->
		<div class="form-group">
			<form action="https://getsimpleform.com/messages?form_api_token=de1ba2f2f947822946fb6e835437ec78" method="post">
			<div class="form-group">
				<input type='text' class="form-control" name='Email' placeholder="Email" required/>
			</div>
			<div>
                        	<button class="btn btn-default" type='submit'>Subscribe</button>
                    	</div>
                	</form>
		</div>
	</div>
</div>

<ul class="social-icons">
	<li>
		<h3>
			<a href="https://twitter.com/our_codingclub" target="_blank">&nbsp;Follow our coding adventures on Twitter! <i class="fa fa-twitter"></i></a>
		</h3>
	</li>
</ul>
