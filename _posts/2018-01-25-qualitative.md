---
layout: post
title: Analysing ordinal data, surveys, count data 
subtitle: Using R to answer sociological questions
date: 2017-01-29 10:00:00
author: Gergana
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

This workshop will explore qualitative data, the sort of data you might collect through responses to survey questions, interview transcripts, or observations. The data analysis techniques in this workshop lend themselves well to sociological research, and the examples we will use come from a study on human behaviour, but they could easily be applied to observations of any system. For example, you might use an ordinal scale (e.g. 1-5, Disagree-Agree) to describe the condition of a plant seedling, with the question being something like "How wilted are the leaves, 1=no sign of damage, 5=leaves abcised". 

Firstly, we will learn how to format data from surveys and interviews effectively so that it can be easily used in analysis later. Knowing a few key data manipulation techniques will make processing the data much faster in the long run. Then we will explore various ways to visualise these data graphically, and finally we will run some simple statistical analyses to answer some hypotheses.

<b>Note : all the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">this repository</a>. Clone and download the repo as a zip file, then unzip it.</b>

Alternatively, you can fork <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">the repository</a> to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our <a href="https://ourcodingclub.github.io/2017/02/27/git.html" target="_blank">previous tutorial.</a>

## Getting Started

The first thing to do is open R Studio. Then make a new script file using `File/ New File/ R Script`, save it with a sensible name inside the folder you just downloaded and unzipped from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>.

Next, in your script file you need to set your working directory to the folder you just downloaded from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>. Copy and paste the code below as a guide, but remember that the path to your folder will be different:

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
This is fake data from an online survey designed to investigate whether gender and different cohabitation arrangements influenced the likelihood of participants performing sustainable actions around the house, like recycling or buying sustainable household products.

This example dataset is formatted purposely to resemble the sort of thing you might generate from your own survey responses. It is not ready for analysis yet! We will spend some time getting the data ready for analysis, so that you can learn skills needed to format your own data for analysis.

## 1. Formatting qualitative data

<a name="format"></a>

Getting qualitative data into the right format for analysis can take some time. Most analytical tools are based on numerical datasets, so some coercion is needed to generate numerical values from our qualitative observations. Designing a survey in the right way to begin with will make analysis much easier later on.

Some of the questions in our data set were designed on a 5 point scale, also known as a Likert scale. Look at the values contained in the column titled: "How often during a normal day do you think about the sustainability of your actions?", by entering this code:

```r
unique(sust_data$sustainability_daily_think)
```

You should see that the column contains 5 discrete categories that follow an order from low to high: `Never`, `Rarely`, `Sometimes`, `Often`, `Nearly every decision I make`. We could just treat the responses as factors, but this doesn't take into account their ordinal nature, so instead we will ask R to treat them as an "ordered factor" using this code:

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


## 2. Visualising qualitative data

<a name="visualise"></a>

Now that we formatted our data for analysis we can visualise the data to identify any interesting patterns. 

Let's start with the likert scales. We can create bar charts to visualise the number of responses to a question which fit into each of the ordinal categories. The correct form for the bar chart will depend on the type of question that was asked, and the wording of the various responses. For example, if potential responses were presented as "Strongly disagree", "Disagree", "Neither agree nor disagree", "Agree", "Strongly agree", you could assume that the neutral or zero answer is in the middle, with Disagree being negative and Agree being positive. On the other hand, if the answers were presented as "Never", "Rarely", "Sometimes", "Often", "Nearly every decision I make", the neutral or zero answer would be Never, with all other answers being positive. For the first example, we could use a "diverging stacked bar chart", and for the latter we would just use a standard "stacked bar chart".




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

