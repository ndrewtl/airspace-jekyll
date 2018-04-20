---
layout: post
title: Analysing ordinal data, surveys, count data 
subtitle: Using R to answer sociological questions
date: 2018-01-29 10:00:00
author: John 
meta: "Tutorials"
tags: datavis data_manip modelling  
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheader_qual.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#format"> 1. Learn how to format survey data, coding responses, data types etc. </a>

#### <a href="#visualise"> 2. Practise visualising ordinal data, count data, likert scales </a>

#### <a href="#text-mining"> 3. Mining text responses and comments for keywords. </a>

#### <a href="#analyse"> 4. Statistically analyse qualitative data</a>

This workshop will explore qualitative data, the sort of data you might collect through responses to survey questions, interview transcripts, or observations. The data analysis techniques in this workshop lend themselves well to sociological research, and the examples we will use come from a study on human behaviour related to environmentally friendly actions, but they could easily be applied to observations of any system. For example, you might use an ordinal scale (e.g. 1-5, Disagree-Agree) to describe the perceived health of a plant seedling, with the question being something like "How wilted are the leaves? 1=no sign of damage, 5=leaves abcised". 

Firstly, we will learn how to format data from surveys and interviews effectively so that it can be easily used in analysis later. Then we will explore ways to visualise these data graphically. Finally we will run some simple statistical analyses to answer some hypotheses.

<b>Note: all the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">this repository</a>. Please clone and download the repo as a zip file, then unzip it before starting the tutorial.</b>

Alternatively, you can fork <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">the repository</a> to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our <a href="https://ourcodingclub.github.io/2017/02/27/git.html" target="_blank">previous tutorial.</a>

## Getting Started

The first thing to do is open RStudio. Then make a new script file using `File/ New File/ R Script`, save it with a sensible name inside the folder you just downloaded and unzipped from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>.

Next, in your script file you need to set your working directory to the folder you just downloaded from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>. Copy and paste the code below as a guide, but remember that the location of the folder on your computer will be different:

```r
setwd("~/Downloads/CC-Qualit-master")
```

Next, load (`library()`) the packages needed for this tutorial by copying the code below into your script file then running those lines through the console. Remember to `install.packages()` if this is the first time you're using these packages:

```r
library(ggplot2)
library(dplyr)
library(tidyr)
library(RColorBrewer)
library(tidytext)
library(R.utils)
library(wordcloud)
```

Finally, load the data files we will be using for the tutorial.

```r
# The survey responses
sust_data <- read.csv("sust_behaviour.csv")

# A lookup table which connects each column in `sust_data` to the actual question on the survey
sust_lookup <- read.csv("sust_lookup.csv")

# A list of boring and non-useful words, bundled with `tidytext`
data(stop_words)
```
This is anonymised data from an online survey designed to investigate whether gender and different cohabitation arrangements influence the likelihood of participants performing environmentally friendly actions around the house, like recycling or buying sustainable household products.

This example dataset is formatted to purposely resemble the sort of thing you might generate from your own survey responses on Google Forms or Survey Monkey. It is not ready for analysis yet! We will spend some time getting the data ready for analysis, so that you can learn the skills needed to format your own data for analysis.

`sust_lookup` is a table which connects the name of each column in the dataframe to the corresponding question that was asked in the survey. Replacing the raw questions with shorter column names makes it much easier to write code, and with the lookup table we can add the actual question title back in when we are creating plots. 

## 1. Formatting qualitative data

<a name="format"></a>

Getting qualitative data into a tidy format for analysis can take some time. Most analytical tools are best suited to numerical datasets, so some coercion is needed to generate numerical values from our qualitative observations. Remember when you are designing a survey to consider how you will analyse the data, this will make it much easier later on.

Some of the questions in this data set were designed on a 5 point scale, also known as a Likert scale. Each column in the dataframe contains responses to a single question. Look at the values contained in the column titled: `sustainability_daily_think`, by entering this code:

```r
unique(sust_data$sustainability_daily_think)
```

You should see that the column contains 5 discrete categories that follow an intuitive order from low to high: `Never`, `Rarely`, `Sometimes`, `Often`, `All the time `. We could just treat the responses as factors, but this doesn't take into account their ordinal nature, any plots that we make will simply place the factors in alphabetical order, so instead we will ask R to treat them as an "ordered factor" using this code:

```r
sust_data$sustainability_daily_think <- factor(sust_data$sustainability_daily_think,
	levels=c("Never", "Rarely", "Sometimes", "Often", "All the time"), 
	ordered=TRUE)
```

Look for other columns that you think contain ordered factor data like this one, then change them to ordered factors in the same way you did above. Search for columns using:

```r
head(sust_data)
```

OR

```r
str(sust_data)
```

Other columns in the data frame, such as sust_data$energy_action, contain strings of letters, e.g. `BDEFH`. This question on the survey presented the user with a list of sustainable actions related to the home, e.g. "I have replaced my lightbulbs with energy saving lightbulbs" and asked the user to tick all the ones that applied to them. Each of the letters refers to a single action. The format of this column is similar to what you would receive if you downloaded the raw results of a Google Form.

Imagine we want to ask the question "Does the number of sustainable energy-related actions performed vary according to gender?". To do this we need to create a column in the data frame which counts the number of letters in `sust_data$energy_action`. To do this we can use `nchar()`, a simple function which counts the number of characters in a string. Additionally, we have to use `as.character()` to coerce `energy_action` to a character variable, as it is currently encoded as a factor, which isn't compatible with `nchar()`.
:

```r
sust_data$energy_action_n <- nchar(as.character(sust_data$energy_action))
```

## 2. Visualising qualitative data

<a name="visualise"></a>

Now that we formatted our data for analysis we can visualise the data to identify some interesting patterns. 

Let's start with the Likert scales. We can create bar charts to visualise the number of responses to a question which fit into each of the ordinal categories. The correct form for the bar chart will depend on the type of question that was asked, and the wording of the various responses. For example, if potential responses were presented as "Strongly disagree", "Disagree", "Neither agree nor disagree", "Agree", "Strongly agree", you could assume that the neutral or zero answer is in the middle, with Disagree being negative and Agree being positive. On the other hand, if the answers were presented as "Never", "Rarely", "Sometimes", "Often", "All the time", the neutral or zero answer would be Never, with all other answers being positive. For the first example, we could use a "diverging stacked bar chart", and for the latter we would just use a standard "stacked bar chart".

### Diverging stacked bar chart

Let's first make a diverging stacked bar chart of responses to the question: "How often during a normal day do you think about the sustainability of your actions?". Investigating how gender affects the response. You can see from the lookup table (`sust_lookup`) that the responses to this question are stored in the column called `sustainability_daily_think`.

Check for yourself by entering the code below to display the contents of the `sust_lookup` object:

```r
sust_lookup
```

If you look in the `sustainability_daily_think` column, you will see that it contains rows like `Often`, `Never`, and `All the time`:

```r
sust_data$sustainability_daily_think
```

First, we need to make a summary data frame of the responses from this column, which can be done easily using the `dplyr` package. For an introduction to `dplyr`, check out <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">our tutorial on data manipulation</a>. Enter the code below to make the summary table: 

```r 
sust_think_summ_wide <- sust_data %>%
	group_by(gender, sustainability_daily_think) %>%
	tally() %>%
	mutate(perc = n / sum(n) * 100) %>%
	dplyr::select(-n) %>%
	group_by(gender) %>%
	spread(sustainability_daily_think, perc)
```

`group_by()` and `tally()` work together to count the number of responses to the question, splitting the count into each combination of gender (e.g. Male, Female) and type of response (e.g. Never, Often, etc.). `mutate()` creates another column called `perc` which is the percentage of the total respondents which responded based on their gender and response. `dplyr::select()` drops the `n` column which was created using `tally()`. The second `group_by()` and `spread()` work together to convert the data frame from long format, to wide format. It's easier to demonstrate what this means with a diagram:

__Long Format:__

<table style="text-align:center; margin:10px">
<tr>
<td colspan="4" style="border-bottom: 1px solid black"></td>
</tr>
<tr>
<td></td>
<td style="padding:0 15px 0 15px">gender</td>
<td style="padding:0 15px 0 15px">sustainability_daily_think</td>
<td style="padding:0 15px 0 15px">perc</td>
</tr>
<tr><td colspan="4" style="border-bottom: 1px solid black"></td></tr>
<tr><td style="padding:0 15px 0 15px">1</td><td>Female</td><td>Never</td><td>1.575</td></tr>
<tr><td style="padding:0 15px 0 15px">2</td><td>Female</td><td>Rarely</td><td>1.575</td></tr>
<tr><td style="padding:0 15px 0 15px">3</td><td>Female</td><td>Sometimes</td><td>32.283</td></tr>
<tr><td style="padding:0 15px 0 15px">4</td><td>Female</td><td>Often</td><td>51.181</td></tr>
<tr><td style="padding:0 15px 0 15px">5</td><td>Female</td><td>All the time</td><td>13.386</td></tr>
<tr><td style="padding:0 15px 0 15px">6</td><td>Male</td><td>Never</td><td>3.226</td></tr>
<tr><td style="padding:0 15px 0 15px">7</td><td>Male</td><td>Rarely</td><td>6.452</td></tr>
<tr><td style="padding:0 15px 0 15px">8</td><td>Male</td><td>Sometimes</td><td>32.258</td></tr>
<tr><td style="padding:0 15px 0 15px">9</td><td>Male</td><td>Often</td><td>38.710</td></tr>
<tr><td style="padding:0 15px 0 15px">10</td><td>Male</td><td>All the time</td><td>19.355</td></tr>
<tr><td colspan="4" style="border-bottom: 1px solid black"></td></tr></table>

__Wide Format:__

<table style="text-align:center; margin:10px"><tr><td colspan="7" style="border-bottom: 1px solid black"></td></tr>
<tr>
<td style="text-align:left"></td>
<td style="padding:0 15px 0 15px">gender</td>
<td style="padding:0 15px 0 15px">Never</td>
<td style="padding:0 15px 0 15px">Rarely</td>
<td style="padding:0 15px 0 15px">Sometimes</td>
<td style="padding:0 15px 0 15px">Often</td>
<td style="padding:0 15px 0 15px">All the time</td>
</tr>
<tr><td colspan="7" style="border-bottom: 1px solid black"></td></tr>
<tr>
<td style="text-align:left">1</td>
<td style="padding:0 15px 0 15px">Female</td>
<td style="padding:0 15px 0 15px">1.575</td>
<td style="padding:0 15px 0 15px">1.575</td>
<td style="padding:0 15px 0 15px">32.283</td>
<td style="padding:0 15px 0 15px">51.181</td>
<td style="padding:0 15px 0 15px">13.386</td>
</tr>
<tr><td style="text-align:left">2</td><td>Male</td><td>3.226</td><td>6.452</td><td>32.258</td><td>38.710</td><td>19.355</td></tr>
<tr><td colspan="7" style="border-bottom: 1px solid black"></td></tr></table>

Basically, in long format each column contains a unique variable (e.g. gender, percentage), whereas in wide format, the percentage data is spread across five columns, where each column is a response type.

And now for the code to create the plot. First, let's have a look at what we are aiming for:

<center> <img src="{{ site.baseurl }}/img/diverging_bar_likert.png" alt="Img" style="width: 800px;"/> </center>

This type of plot is called a diverging stacked bar chart. "Stacked" means that each bar is further split into sub-categories, in this case each bar is a gender and each sub-bar is the percentage of that gender giving a particular response. "Diverging" means that the bar is straddled over the zero line. Formatting the bar chart in this way allows us to make a visual distinction between negative responses (i.e. Never, Rarely), positive responses (i.e. Often, All the time) and neutral responses (i.e. Sometimes). It is unfortunately not straightforward to achieve a plot like this, it requires some `ggplot2` trickery.

The main problem is getting the "Sometimes" responses to straddle the 0 line. To do this, we have to split the "Sometimes" values into two groups (`midlow` and `midhigh`), one group will sit below the zero line and one group will sit above. To do this we can use `dplyr` again:


```r
sust_think_summ_hi_lo <- sust_think_summ_wide %>%
	mutate(midlow = Sometimes / 2,
		midhigh = Sometimes / 2) %>%
	dplyr::select(gender, Never, Rarely, midlow, midhigh, Often, `All the time`) %>%
	gather(key = response, value = perc, 2:7) %>%
	`colnames<-`(c("gender", "response", "perc"))
```

In the code above we have created two new columns `midhigh` and `midlow`, which both contain values from `Sometimes`, but divided by 2. The `Sometimes` column is then dropped from the data frame using `dplyr::select()`. The data frame is then gathered back into long format so there are three columns, gender, response type, and percentage of respondents.

Next, we have to split the data frame into two data frames, one containing the negative responses and half of `Sometimes` (i.e. `midlow`) and one containing the positive repsonses and the other half of `Sometimes` (i.e. `midhigh`). We need to do this because there are actually two sets of bars on the graph, one for the left side of the zero line and one for the right of the zero line.

The code below creates two new data frames. `%in%` allows us to search for multiple matches in the `response` column, whereas `==` only allows us to search for one response:

```r
sust_think_summ_hi <- sust_think_summ_hi_lo %>%
	filter(response %in% c("All the time", "Often", "midhigh")) %>%
	mutate(response = factor(response, levels = c("All the time", "Often", "midhigh")))

sust_think_summ_lo <- sust_think_summ_hi_lo %>%
	filter(response %in% c("midlow", "Rarely", "Never")) %>%
	mutate(response = factor(response, levels = c("Never", "Rarely", "midlow")))
```

Next, in order to change the colours on the plot, we need to define a custom colour scheme. To do this I'm using a colour palette from `RColorBrewer` and tweaking it a bit.

```r
# Use RColorBrewer to store a preset diverging colour palette as a vector of colour codes 
legend_pal <- brewer.pal(name = "RdBu", n = 5)

# Duplicate the middle value, remember that "Sometimes" is actually two groups, "midhigh" and "midlow"
legend_pal <- insert(legend_pal, ats = 3, legend_pal[3])

# Replace the ugly white colour for "Sometimes" with a pleasant dishwater grey
legend_pal <- gsub("#F7F7F7", "#9C9C9C", legend_pal)

# Assign names to the vector based on the colours we want for each group
names(legend_pal) <- c("All the time", "Often", "midhigh", "midlow", "Rarely", "Never" )
```

Now for the actual plot code!

```r
ggplot() + 
	geom_bar(data=sust_think_summ_hi, aes(x = gender, y=perc, fill = response), stat="identity") +
	geom_bar(data=sust_think_summ_lo, aes(x = gender, y=-perc, fill = response), stat="identity") + 
	geom_hline(yintercept = 0, color =c("black")) + 
	scale_fill_manual(values = legend_pal, 
		breaks = c("All the time", "Often", "midhigh", "Rarely", "Never"),
		labels = c("All the time", "Often", "Sometimes", "Rarely", "Never")) +
	coord_flip() + 
	labs(x = "Gender", y = "Percentage of respondents (%)") + 
	ggtitle(sust_lookup$survey_question[sust_lookup$column_title == "sustainability_daily_think"]) +
	theme_classic() 
```

as you can see there are two `geom_bar()` arguments, one for the positive responses and one for the negative responses. `geom_hline()` makes the 0 line. `scale_fill_manual()` applies the colour scheme. Notice that `breaks =` is a vector of colour values that will be included in the legend, and `labels =` gives them custom names, in this case, turning "midhigh" to "Sometimes" and excluding `midlow` entirely. `coord_flip()` rotates the whole plot 90 degrees, meaning the bars are now horizontal. `labs()` and `ggtitle()` define the custom x and y axis labels and the title. `ggtitle()` accesses the lookup table to display the name of the question from the name of the column in our original data frame. `theme_classic() just makes the whole plot look nicer, removing the default grey background.

Of course, there are other options to display this sort of data. You could use a pie chart, or just a basic table showing the number of responses by group, but I think that the diverging bar chart gives an effective way to compare groups of respondees, or even to compare answers to different questions, if you group by question instead of gender.


### Basic stacked bar chart

For the second example, to demonstrate a conventional stacked bar chart, it is much easier. We will use the question on "How many of these energy related sustainable actions do you perform?", the responses to which are found in `sust_data$energy_action`.

First, we need to count the number of sustainable actions performed, like we did earlier:

```r
sust_data$energy_action_n <- nchar(as.character(sust_data$energy_action))
```

Then we can define a custom colour palette for red and blue and name the colours after our gender categories:

```r
male_female_pal <- c("#0389F0", "#E30031")
names(male_female_pal) <- c("Male", "Female")
```

Then create the plot:

```r
ggplot(sust_data, aes(x =energy_action_n, fill = gender)) + 
	geom_bar() + 
	scale_fill_manual(values = male_female_pal) + 
	scale_x_continuous(breaks = seq(1:8)) +
	theme_classic()
```

<center> <img src="{{ site.baseurl }}/img/stacked_bar_qual.png" alt="Img" style="width: 800px;"/> </center>


### Bubble plot

If we want to compare correlations between two categories of data, we can use a bubble plot. For example, is there a pattern between age of respondent and how often they think about sustainable activities? Unfortunately, the data from this survey doesn't contain actual age values, only age ranges (e.g. 18-20, 21-29 etc.). 

First, create a summary table by tallying the number of responses by the two groups, age and how often they think about sustainable activities:

```r
sust_bubble <- sust_data %>%
	group_by(age, sustainability_daily_think) %>%
	tally()
```

Then to create the bubble plot, simply adjust the size of points according to their frequency of occurrence (`n`):

```r
ggplot(sust_bubble, aes(x = age, y = sustainability_daily_think)) +
	geom_point(aes(size = n)) + 
	theme_classic()
```

<center> <img src="{{ site.baseurl }}/img/bubble_chart_qual.png" alt="Img" style="width: 800px;"/> </center>

## 3. Mining text responses and comments for keywords 

<a name="text-mining"></a>

As well as the tick box style questions, some questions in our survey asked for free-hand text comments. These comments give some extra information and context to survey responses and shouldn't be ignored. As an example, look at the column `energy_action_comment` by typing:

```r
sust_data$energy_action_comment
```

We can mine the comments for keywords to build up a more complete picture of what our respondents were thinking about when they did the survey and whether that varies by gender. To make the comments easier to work with, we should make the data "tidy" by splitting each comment so that each row has a single word only. 

### Comments from all the questions 

The following pipe collects all the comment columns along with the gender and id columns (`dplyr::select()`), then gathers those comment columns together into a single column (`gather()`), then transforms the comments column from a factor into a character class (`mutate()`). 

```r
sust_comm_gather <- sust_data %>% 
	dplyr::select(id, gender, energy_action_comment, 
		food_action_comment, water_action_comment, 
		waste_action_comment, other_action_comment) %>%
	gather(action, comment, -id, -gender) %>%
	mutate(comment = as.character(comment))
```

The next pipe takes that gathered data and uses `unnest_tokens()` from the `tidytext` package to split the comments so that there is only one word per row, then it uses the list of boring words from the `stop_words` object that we loaded earlier to remove those words from our dataset (`anti_join()`). Then it counts the number of occurrences of each unique word in the `comment_word` column. Finally a bit of tidying in the form of removing words which occur less than 5 times (`filter(n > 5)`) and removing NA values (`filter(!is.na(comment_word))`): 
```r
sust_comm_tidy <- sust_comm_gather %>%
	group_by(gender) %>%
	unnest_tokens(output = comment_word,
		input = comment) %>%
	anti_join(stop_words, by = c("comment_word" = "word")) %>%
	count(comment_word, sort = TRUE)  %>%
	filter(n > 10) %>%
	filter(!is.na(comment_word)) 
```

Now it is easy to plot the occurrences of each word, and colour by gender (`fill = gender`), using `ggplot()`:

```r
ggplot(sust_comm_tidy, aes(x = comment_word, y = n, fill = gender)) + 
	geom_bar(stat = "identity") + 
	coord_flip() + 
	scale_fill_manual(values = male_female_pal) + 
	theme_classic()
```

<center> <img src="{{ site.baseurl }}/img/comment_gender_qual.png" alt="Img" style="width: 800px;"/> </center>

### Comments from a single question

We might also want to investigate a single question's comments in more detail. For example, the `energy_action_comment` column. First repeat the action of converting to character format (`mutate()`), then split the column so each row is one word (`unnest_tokens()`), then remove boring words (`antijoin()`), and count the frequency of each word:

```
tidy_energy_often_comment <- sust_data %>%
	mutate(energy_action_comment = as.character(energy_action_comment)) %>%
	unnest_tokens(output = energy_action_comment_word,
		input = energy_action_comment) %>%
	anti_join(stop_words, by = c("energy_action_comment_word" = "word")) %>%
	count(energy_action_comment_word, sort = TRUE) 
```

Then keep only the most common words and plot it as a bar chart:

```r
tidy_energy_often_comment_summ <- tidy_energy_often_comment %>%
	filter(n > 10) %>%
	filter(!is.na(energy_action_comment_word)) %>%
	mutate(energy_action_comment_word = reorder(energy_action_comment_word, n ))

ggplot(tidy_energy_often_comment_summ, aes(x = energy_action_comment_word, y = n)) +
	geom_col() +
	xlab(NULL) +
	coord_flip() + 
	theme_classic()
```

<center> <img src="{{ site.baseurl }}/img/word_bar_qual.png" alt="Img" style="width: 800px;"/> </center>

### Wordclouds

To effectively plot more words and their frequencies, you could also create a word cloud:

```r
tidy_energy_often_comment %>%
	with(wordcloud(words = energy_action_comment_word, freq = n, max.words = 100))
```

<center> <img src="{{ site.baseurl }}/img/wordcloud_qual.png" alt="Img" style="width: 800px;"/> </center>

For more on text mining using `tidytext` I would highly recommend <a href="https://www.tidytextmining.com" target="_blank">their Gitbook website</a>, which has some good tutorials and goes into far more depth than we have time for here..

<a name="analyse"></a>

## 4. Analyse qualitative data

Visualising qualitative data can take you a long way, and can often give more useful information than statistical analysis, but sometimes statistical analysis is needed before you can definitively prove or disprove a hypothesis. Due to the way survey data are often formatted, with lot of counts and factors, the assumptions of conventional parametric statistical analysis are often violated, necessitating a more complex statistical approach. Below are a few examples of how to test various hypotheses in our survey data. 

### Chi-squared

To test if there is a statistically significant correlation between gender and how often sustainable tasks are though about, we can use a chi-squared test of independence.

```r
gender_think_chi <- chisq.test(sust_data$gender, sust_data$sustainability_daily_think)
gender_think_chi
```

The output of the `gender_think_chi` object can be used to interpret the outcome of the chi-squared test, with a lower p-value indicating a greater probability that the two variables are dependent on each other. In this case, p = 0.01518, which is lower than the conventional threshold of 0.05, meaning we can reject the null hypothesis that gender does not correlate with the frequency that sustainable tasks are thought about.

### Poisson regression

For a more in depth analysis, we might hypothesise that gender causes the difference in the number of energy related sustainable actions performed. This is in contrast to the Chi-squared test which merely suggests a non-directional correlative tendency between the two variables. As the number of actions performed is count data, we can use a poisson regression, which is a form of generalised linear model: 

```r
energy_action_pois <- glm(energy_action_n ~ gender, family = "poisson", data = sust_data)
summary(energy_action_pois)
```

In this case it seems like there actually isn't much effect of gender on number of actions performed, with a very low z-value of 0.343 and a non-significant p-value (0.732). This means I would be inclined to accept a null hypothesis that gender does not affect the number of sustainable energy actions performed. 

### Multi-variate poisson regression

Going deeper, we might hypothesise that gender and age interact to determine the amount of sustainable food related actions. For example, maybe the difference between genders becomes more accentuated as age increases. Including age in our model might help to make the model fit better and explain more variance. This effect can be included in a generalised linear model as an "interaction term". In the code below `gender * age` defines the interaction between those two explanatory variables:

```r
energy_action_pois_int <- glm(energy_action_n ~ gender * age, family = "poisson", data = sust_data)
summary(energy_action_pois_int)
```

Unfortunately we still have no significant p-values, and additionally it seems like adding that extra variable hasn't added to the quality of the model. Comparing the AIC values, the original model has a smaller AIC than the more complex model, meaning that the original model is generally of better fit and quality. 


<hr>
<hr>

<h3><a href="https://www.surveymonkey.co.uk/r/83WV8HV" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
<br>
<h3>&nbsp; You can contact us with any questions on <a href="mailto:ourcodingclub@gmail.com?Subject=Tutorial%20question" target = "_top">ourcodingclub@gmail.com</a></h3>
<br>
<h3>&nbsp; Related tutorials:</h3>
{% for post in site.posts %}
	{% if post.url != page.url %}
  		{% for tag in post.tags %}
    			{% if page.tags contains tag %}
<h4><a style="margin:0 padding:0" href="{{ post.url }}">&nbsp; - {{ post.title }}</a></h4> 
  			{% endif %} 
		{% endfor %}
	{% endif %}
{% endfor %}
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

