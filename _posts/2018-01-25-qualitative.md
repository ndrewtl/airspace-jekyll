---
layout: post
title: Analysing ordinal data, surveys, count data 
subtitle: Using R to answer sociological questions
date: 2017-01-29 10:00:00
author: John 
meta: "Tutorials"
tags: datavis data_manip modelling  
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheaderqual.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#format"> 1. Learn how to format survey data, coding responses, data types etc. </a>

#### <a href="#visualise"> 2. Practice visualising ordinal data, count data, likert scales </a>

#### <a href="#analyse"> 3. Statistically analyse qualitative data</a>

This workshop will explore qualitative data, the sort of data you might collect through responses to survey questions, interview transcripts, or observations. The data analysis techniques in this workshop lend themselves well to sociological research, and the examples we will use come from a study on human behaviour related to environmentally friendly actions, but they could easily be applied to observations of any system. For example, you might use an ordinal scale (e.g. 1-5, Disagree-Agree) to describe the condition of a plant seedling, with the question being something like "How wilted are the leaves? 1=no sign of damage, 5=leaves abcised". 

Firstly, we will learn how to format data from surveys and interviews effectively so that it can be easily used in analysis later. Knowing a few key data manipulation techniques will make processing the data much faster in the long run. Then we will explore ways to visualise these data graphically. Finally we will run some simple statistical analyses to answer some hypotheses.

<b>Note : all the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">this repository</a>. Clone and download the repo as a zip file, then unzip it.</b>

Alternatively, you can fork <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">the repository</a> to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our <a href="https://ourcodingclub.github.io/2017/02/27/git.html" target="_blank">previous tutorial.</a>

## Getting Started

The first thing to do is open RStudio. Then make a new script file using `File/ New File/ R Script`, save it with a sensible name inside the folder you just downloaded and unzipped from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>.

Next, in your script file you need to set your working directory to the folder you just downloaded from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>. Copy and paste the code below as a guide, but remember that the location of th folder on your computer will be different:

```r
setwd("~/Downloads/CC-Qualit-master")
```

Next, load (`library()`) the packages needed for this tutorial by copying the code below into your script file then running those lines through the console. Remember to `install.packages()` if this is the first time you're using these packages:

```r
library(ggplot2)
library(dplyr)
```

Finally, load the data files we will be using for the tutorial.

```r
sust_data <- read.csv("sust_behaviour.csv")
```
This is fake data from an online survey designed to investigate whether gender and different cohabitation arrangements influenced the likelihood of participants performing environmentally friendly actions around the house, like recycling or buying sustainable household products.

This example dataset is formatted purposely to resemble the sort of thing you might generate from your own survey responses, on Google Forms or Survey Monkey. It is not ready for analysis yet! We will spend some time getting the data ready for analysis, so that you can learn the skills needed to format your own data for analysis.

## 1. Formatting qualitative data

<a name="format"></a>

Getting qualitative data into the right format for analysis can take some time. Most analytical tools are best suited to numerical datasets, so some coercion is needed to generate numerical values from our qualitative observations. Remember when you are designing a survey to consider how you will analyse the data, this will make it much easier later on.

Some of the questions in this data set were designed on a 5 point scale, also known as a Likert scale. Look at the values contained in the column titled: "sustainability_daily_think", by entering this code:

```r
unique(sust_data$sustainability_daily_think)
```

You should see that the column contains 5 discrete categories that follow an intuitive order from low to high: `Never`, `Rarely`, `Sometimes`, `Often`, `Nearly every decision I make`. We could just treat the responses as factors, but this doesn't take into account their ordinal nature, any plots that we make will simply place the factors in alphabetical order, so instead we will ask R to treat them as an "ordered factor" using this code:

```r
sust_data$sustainability_daily_think <- factor(sust_data$sustainability_daily_think, 
levels=c("Never", "Rarely", "Sometimes", "Often", "Nearly every decision I make"), 
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

Other columns in the data frame, such as sust_data$energy_action, contain strings of letters, e.g. `BDEFH`. This question on the survey presented the user with a list of sustainable actions related to the home, e.g. "I have replaced my lightbulbs with energy saving lightbulbs" and asked the user to tick all the ones they had done. Each of the letters refers to a single action. The format of this column is similar to what you would receive if you downloaded the raw results of a Google Form.

Imagine we want to ask the question "Does the number of sustainable energy-related actions performed vary depending on gender?". To do this we need to create a column in the data frame which counts the number of letters in `sust_data$energy_action`. To do this we can use `nchar()`, a simple function which counts the number of characters in a string. Additionally, we have to use `as.character()` to coerce `energy_action` to a character variable, as it is currently encoded as a factor, which isn't compatible with `nchar()`.
:

```r
sust_data$energy_action_n <- nchar(as.character(sust_data$energy_action))
```

Finally, some columns (e.g. `energy_action_comment`) contain comments left by people who completed the survey, giving some extra information or giving context to their answers. We can mine these comments for keywords to build up a more complete of what our respondents were thinking about when they did the survey and whether that varies by gender.

```r
sust_comment <- sust_data %>% 
	select(id, gender, energy_action_comment, 
				 food_action_comment, water_action_comment, 
				 waste_action_comment, other_action_comment) %>%
	gather(action, comment, -id, -gender) %>%
	mutate(comment = as.character(comment)) %>% 
	group_by(gender) %>%
	unnest_tokens(output = comment_word,
								input = comment) %>%
	anti_join(stop_words, by = c("comment_word" = "word")) %>%
	count(comment_word, sort = TRUE)  %>%
	filter(n > 5) %>%
	filter(!is.na(comment_word)) %>% 
	mutate(comment_word = reorder(comment_word, n)) 

sust_comment$comment_word <- reorder(sust_comment$comment_word, sust_comment$n)

ggplot(sust_comment, aes(x = comment_word, y = n, fill = gender)) + 
	geom_bar(stat = "identity") + 
	coord_flip()


https://www.tidytextmining.com

## 2. Visualising qualitative data

<a name="visualise"></a>

Now that we formatted our data for analysis we can visualise the data to identify some interesting patterns. 

Let's start with the likert scales. We can create bar charts to visualise the number of responses to a question which fit into each of the ordinal categories. The correct form for the bar chart will depend on the type of question that was asked, and the wording of the various responses. For example, if potential responses were presented as "Strongly disagree", "Disagree", "Neither agree nor disagree", "Agree", "Strongly agree", you could assume that the neutral or zero answer is in the middle, with Disagree being negative and Agree being positive. On the other hand, if the answers were presented as "Never", "Rarely", "Sometimes", "Often", "Nearly every decision I make", the neutral or zero answer would be Never, with all other answers being positive. For the first example, we could use a "diverging stacked bar chart", and for the latter we would just use a standard "stacked bar chart".

As an example, let's first make a diverging stacked bar chart of responses to the question: "How often during a normal day do you think about the sustainability of your actions?". Investigating how gender affects the response. You can see from the lookup table (`sust_lookup`) that the responses to this question are stored in the column called `sustainability_daily_think`.

Check for yourself by entering the code below to display the contents of the `sust_lookup` object:

```r
sust_lookup
```

First, we need to make a summary data frame of the responses from this column, which can be done easily using the `dplyr` package. For an introduction to `dplyr`, check out <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">our tutorial on data manipulation</a>. Enter the code below to make the summary table: 

```r 
sust_think_summ <- sust_data %>%
	group_by(gender, sustainability_daily_think) %>%
	tally() %>%
	mutate(perc = n / sum(n) * 100) %>%
	dplyr::select( -n) %>%
	group_by(gender) %>%
	spread(sustainability_daily_think, perc)
```

`group_by()` and `tally()` work together to count the number of responses to the question, splitting the count into each combination of gender (e.g. Male, Female) and type of response (e.g. Never, Often, etc.). `mutate()` creates another column called `perc` which is the percentage of the total respondents which responded based on their gender and response, `dplyr::select()` drops the `n` column which was created using `tally()`. The second `group_by()` and `spread()` work together to convert the data frame from long format, to wide format. It's easier to demonstrate what this means with a diagram:

__INSERT DIAGRAM__


And now for the code to create the plot. First, let's have a look at what we are aiming for:

__INSERT_PLOT__

This type of plot is called a diverging stacked bar chart. "Stacked" means that each bar is further split into sub-categories, in this case ech bar is a gender and each sub-bar is the percentage of that gender giving a particular response. "Diverging" means that the bar is straddled over the 0 line. Formatting the bar chart in this way allows us to make a visual distinction between negative responses (i.e. Never, Rarely), positive responses (i.e. Often, All the time) and neutral responses (i.e. Sometimes). It is unfortunately not straightforward to achieve a plot like this, it requires some `ggplot2` trickery.

The main problem is getting the "Sometimes" responses to straddle the 0 line. To do this, we have to split the "Sometimes" values into two groups, one group will sit below the 0 line and one group will sit above. To do this we can use `dplyr` again:


```r
sust_think_summ_hi_lo <- sust_think_summ %>%
	mutate(midlow = Sometimes / 2,
		midhigh = Sometimes / 2) %>%
	dplyr::select(gender, Never, Rarely, midlow, midhigh, Often, `All the time`) %>%
	gather(key = gender, value = perc) %>%
	`colnames<-`(c("gender", "response", "perc"))
```

In the code above we have created two new columns `midhigh` and `midlow`, which both contain values from `Sometimes`, but divided by 2. The `Sometimes` column is then dropped from the data frame using `dplyr::select()`. The data frame is then gathered back into long format so there are three columns, gender, response type, and percentage of respondents.

Next, we have to split the data frame into two data frames, one containing the negative responses and half of `Sometimes` (i.e. `midlow`) and one containing the positive repsonses and the other half of `Sometimes` (i.e. `midhigh`). We need to do this because there are actually two sets of bars on the graph, one for the left side of the 0 line and one for the right of the 0 line.

The code below creates two new data frames

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

# Copy the middle value, remember that "Sometimes" is actually two groups, "midhigh" and "midlow"
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
	ggtitle(question_lookup$survey_question[question_lookup$column_title == "sustainability_daily_think"]) +
	theme_classic() 
```

as you can see there are two `geom_bar()` arguments, one for the positive responses and one for the negative responses. `geom_hline()` makes the 0 line. `scale_fill_manual()` applies the colour scheme. Notice that `breaks =` is a vector of colour values that will be included in the legend, and `labels =` gives them custom names, in this case, turning "midhigh" to "Sometimes". `coord_flip()` rotates the whole plot 90 degrees, meaning the bars are now horizontal. `labs()` and `ggtitle()` define the custom x and y axis labels and the title. `ggtitle()` accesses the lookup table to display the name of the question from the name of the column in our original data frame. `theme_classic() just makes the whole plot look nicer, removing the default grey background.

For the second example it is much easier. Just create the summary table and plot as a normal stacked bar chart, without any of the fiddling to get the neutral option to display in the 0 mark.

__DOT PLOT OF MATRIX OF RESPONSES__

Of course, there are other options to display this sort of data. You could use a pie chart, or just a basic table showing the number of responses by group, but I think that the diverging bar chart gives an effective way to compare groups of respondees, or even to compare answers to different questions, if you group by question instead of gender.

## 3. Analyse qualitative data

<a name="analyse"></a>






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

