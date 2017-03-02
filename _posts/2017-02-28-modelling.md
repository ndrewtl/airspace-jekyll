---
layout: post
title: From distributions to linear models
subtitle: Getting comfortable with the basics of statistics modelling
date: 2017-02-28 08:00:00
author: Gergana
meta: "Tutorials"
---

<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheaderlm.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#distributions"> 1. Get familiar with different data distributions</a>

#### <a href="#linear"> 2. Practice linear models</a>

#### <a href="#generalised"> 2. Practice generalised linear models</a>

As you are setting out to answer your research questions, often you might want to know what is the effect of X on Y, how does X change with Y, etc. The answer to "What statistical analysis are you going to use?" will probably be a model of some sort. A model in its simplest forms looks like: 

`temp.m <- lm(soil.temp ~ elevation)` - i.e. we are trying to determine the effect of elevation on soil temperature. 

A slightly more complicated model might look like: `skylark.m <- lm(abundance ~ treatment + farm.area, family = poisson, data = skylarks)` - here you are modelling `abundance`, the response variable, as a function of `treatment` (e.g. a categorical variable describing different types of farms) and `farm.area` (i.e. the size of each farm on which abundance data were collected) - those are your explanatory variables. The `family` argument refers to the distribution of the data, in this case `abundance` represents count zero-inflated data, for which a Poisson distribution is suitable. The `data` argument refers to the dataframe from which the variables we are studying come.

We will talk more about different data distributions later, until then, __go to <a href = "https://github.com/ourcodingclub/CC-8-Modelling">the repository for this tutorial</a>, fork it to your own Github account, clone the repository on your computer and start a version-controlled project in RStudio. For more details on how to do this, please check out our <a href = "https://ourcodingclub.github.io/2017/02/27/git.html"> Intro to Github for version control</a> tutorial.__

Here is a brief summary of the data distributions you might encounter most often.

### Different data distributions

<a name="distributions"></a>

#### __Gaussian__ - Continuous data (normal distribution and homoscedasticity provided)
#### __Poisson__ - Count abundance data (integer values, zero-inflated data, left-skewed data)
#### __Binomial__ - Binary variables (TRUE / FALSE, 0/1, presence / absence data)

Choosing the right distribution for your analysis is an important step about which you should think carefully - it could be frustrating to spend tons of time running models, plotting their results and writing them up only to realise that all along you should have used e.g. a Poisson distribution instead of a Gaussian one.

Another important to consider aspect of modelling is how many terms, i.e. explanatory variables, you want your model to include. It's a good idea to draft out your model structure before you have started thinking about exactly which R packages you will use, running different types of models, etc. Think about what it is you want to examine and what are the potential confounding variables, i.e. what else might influence your response variable, aside from the explanatory variable you are most interested in? Here is an example model structure:

```r
skylark.m <- lm(abundance ~ treatment + farm.area + latitude + longitude + visits)
```

Here we are chiefly interested in the effect of treatment - does skylark abundance vary between the different farm treatments? This is the research question we might have set out to answer, but we still need to acknowledge that farm treatment type is not the only factor influencing abundance. Based on our ecological understanding, we can select other potentially confounding variables - for example skylark abundance will most likely be higher on larger farms - we need to account for that. Additionally, where farms are located might have an effect, thus we are adding `latitude + longitude`. Imagine your experimental design didn't go exactly as you planned - you meant to visit all farms three times to collect data, but some farms you managed to visit only twice. Ignoring this would weaken your final results - is abundance different / the same because the treatment has no / an effect, or because there were differences in study effort? To test that, you can include a `visits` term examining the effect of number on visits on abundance. Some might say this model is very complex, and they would be right - there are a lot of terms in it! A simple model is usually prefered to a complex model, but if you have strong reasons for including a term in your model, then it should be there. So think carefully about your model structure - once you know the variables whose effects you want to study, and the variables whose effects you might need to account for, you can move onto running your models.

If your model has a lot of variables, you are also in danger of __overfitting__ - meaning that you have many variables, but there simply is not enough variation in your data set to account for including all of them. Overfitting can cast doubt over your model's output, so think carefully about the structure of your model

We will now explore a few different types of models.

<a name="linear"></a>

### Practicing linear models

Open the `Modelling_script.R` file and add in your details. We will start by working with a sample dataset about apple yield in relation to different factors. The dataset is part of the `agridat` package.

```r
install.packages("agridat")
library(agridat)

# Loading the dataset from agridat
apples <- agridat::archbold.apple
head(apples)
summary(apples)
```
Check out the dataset. Before we run our model, it's a good idea to visualise the data just to get an idea of what to expect. We can make a boxplot for this purpose. We can examine the effect of spacing on apple yield - we can hypothesise that the closer apples are to other apples, the more they compete for resources, thus reducing their yield. Ideally, we would have sampled yield from many orchards where the trees were planted at different distances from one another - from the summary of the dataset you can see that there are only three `spacing` categories - 6, 10 and 14 m, it would be a bit of a stretch to count three numbers as a continuous variable, so let's make them a factor instead. This turns the previously numeric `spacing` variable into a 3-level categorical variable, with 6, 10 and 14 being its levels.

```r
apples$spacing2 <- as.factor(apples$spacing)

(apples.p <- ggplot(apples, aes(spacing2, yield)) +
    geom_boxplot(fill = "#CD3333", alpha = 0.8, colour = "#8B2323") +
    theme.clean() +  
    theme(axis.text.x = element_text(size = 12, angle = 0)) +
  labs(x = "Spacing (m)", y = "Yield (kg)"))
```

<center><img src="{{ site.baseurl }}/img/apples2.png" alt="Img" style="width: 700px;"/></center>

From our boxplot we can see that yield is pretty similar across the different spacing distances - even though there is a trend towards higher yield at higher spacing, the error bars almost completely overlap. From looking at this boxplot alone, one might image our hypothesis of higher yield at higher spacing not being supported. Let's run a model to explicitly test this.

```r
apples.m <- lm(yield ~ spacing2, data = apples)
summary(apples.m)
```
Check out the summary output of our model:

<center><img src="{{ site.baseurl }}/img/output.png" alt="Img" style="width: 800px;"/></center>

Turns out that yield does significantly differ between the three spacing categories - we can reject the null hypothesis of no effect of spacing on apple yield. It looks like apple yield is indeed higher when the distance between trees is higher - this is in line with our original ecological thoughts - the further away trees are from one another, the less they are limiting each others growth. But let's take a look at a few other things from the summary output. Notice how because `spacing2` is a factor, you get results for `spacing210`, `spacing214`. If you are looking for the `spacing26` category, that is the intercept - R just picks the first category in an alphabetical order and makes that one the intercept. You also get a `Multiple R-squared` value, and an `Adjusted R-squared` value. These values refer to how much of the variation in the `yield` variable is explained by our predictor `spacing2` - the values go from 0 to 1, with 1 meaning that our model variables explain 100% of the variation in the examined variable. `R-squared` values tend to increase as you add more terms to your model, but you also need to account for overfitting - the `Adjusted R-squared` value takes into account how many terms your model has, and how many data points are available in the response variable. From looking at our `R-squared` values, this is not a great model, which makes sense - imagine all the other things that could have an impact on yield that we have not studied - fertilisation levels, weather conditions, water availability, etc.

In addition to checking whether this model makes sense from an ecological perspective, we should check that it actually meets the assumptions of a linear model:

```r

# Checking that the residuals are normally distributed
apples.resid <- resid(apples.m)
shapiro.test(apples.resid)
# Normal distribution

# Checking for homoscedasticity
bartlett.test(apples$yield, apples$spacing2)
bartlett.test(yield ~ spacing2, data = apples)  # Note that these two ways of writing the code give the same results
# Homoscedasticity
```

Linear model assumptions are met (we can imagine that the data points are independent, since we didn't collect the data, we can't really know).

We can examine the model fit further by looking at a few plots:
```r
plot(apples.m)
```

This will produce a set of four plots: residuals versus fitted values, a Q-Q plot of standardized residuals, a scale-location plot (square roots of standardized residuals versus fitted values, and a plot of residuals versus leverage that adds bands corresponding to Cook's distances of 0.5 and 1. In general, looking at these plots can help you identify any outliers that have huge leverage, and confirm that your model has ran alright - e.g. you would want the data points on the Q-Q plot to follow the line.

### Practicing generalised linear models

The model we used above was a __general__ linear model, since it met all the assumptions for one (normal distribution, homoscedasticity, etc.) Quite often in ecology and environmental science that is not the case, and then we use different data distributions. Here we will talk about a Poisson and a binomial distribution - to use them, we need to run __generalised__ linear models.

#### A model with a Poisson distribution

Import the `shagLPI.csv` dataset and check it's summary using `summary(shagLPI)` - notice that for some reason R has decided that year is a character variable, when it should instead be a numeric variable. Let's fix that, so that we don't run into trouble later. The data represent population trends for European Shags on the Isle of May, and are available from the <a href = "http://www.livingplanetindex.org/home/index">Living Planet Index.</a>

```r
shag$year <- as.numeric(shag$year)

# Making a histogram to asses data distribution
shag.hist <- ggplot(shag, aes(pop)) + geom_histogram() + theme.clean()
```

<center><img src="{{ site.baseurl }}/img/poisson2.png" alt="Img" style="width: 700px;"/></center>

Our `pop` variable represents count abundance data, i.e. integer values (whole European Shags!), so a Poisson distribution is appropriate. Often count abundance data are zero-inflated and skewed towards the right - here our data are not like that, but if they were, a Poisson distribution would still have been appropriate.

```r
shag.m <- glm(pop ~ year, family = poisson, data = shag)
summary(shag.m)
```

From the summary of our model we can see that European Shag abundance varies significantly based on the predictor `year`. Let's visualise how European Shag abundance has changed through the years:

```r
(shag.p <- ggplot(shag, aes(x = year, y = pop)) +
    geom_point(colour = "#483D8B") +
    geom_smooth(method = glm, colour = "#483D8B", fill = "#483D8B", alpha = 0.6) +
    scale_x_continuous(breaks = c(1975, 1980, 1985, 1990, 1995, 2000, 2005)) +
    theme.clean() +
    labs(x = " ", y = "European Shag abundance"))
```

<center><img src="{{ site.baseurl }}/img/shag.png" alt="Img" style="width: 700px;"/></center>

__Figure 1. European shag abundance on the Isle of May, Scotland, between 1970 and 2006.__ Points represent raw data and model fit represents a generalised linear model with 95% confidence intervals.

#### A model with a binomial distribution

We will now work this the `Weevil_damage.csv` data that you can import from your project's directory. We can examine if damage to Scott's pine by weevils (a binary, TRUE/FALSE variable) varies based on the block in which the trees were located. You can imagine that different blocks represent different Scott's pine populations, perhaps some of them will be particularly vulnerable to weevils?

```r
# Making block a factor (a categorical variable)
Weevil_damage$block <- as.factor(Weevil_damage$block)

# Running the model
weevil.m <- glm(damage_T_F ~ block, family = binomial, data = Weevil_damage)
summary(weevil.m)
```

Check out the summary output - looks like the probability of a pine tree enduring damage from weevils does vary significantly based on the block in which the tree was located.

<b> We have now covered the basics of modelling - in our next tutorial we will look at mixed effects models, which are used more and more within ecology and environmental science. Until then, you can check out a couple of other tutorials on modelling to further your knowledge:

<a href = "http://data.princeton.edu/R/linearModels.html"> General and generalised linear models, by Germán Rodríguez. </a>

<a href = "http://tutorials.iq.harvard.edu/R/Rstatistics/Rstatistics.html"> Regression modelling in R, by Harvard University. </a>

<hr>
<hr>

#### Check out our <a href="https://ourcodingclub.github.io/links/">Useful links</a> page where you can find loads of guides and cheatsheets.

#### If you have any questions about completing this tutorial, please contact us on ourcodingclub@gmail.com

#### We would love to hear your feedback on the tutorial, whether you did it in the classroom or online: 
#### [https://www.surveymonkey.co.uk/r/NNRS98G](https://www.surveymonkey.co.uk/r/NNRS98G)
