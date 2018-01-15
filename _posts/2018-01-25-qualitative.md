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

#### <a href="#format"> 1. Learn how to format survey data, coding responses </a>

#### <a href="#visualise"> 2. Practice visualising ordinal data, count data, likert scales </a>

#### <a href="#analyse"> 3. Statistically analyse qualitative data</a>

This workshop will explore qualitative data, such as the sort of data you might collect through responses to survey questions, interview transcripts, or observations. The data analysis techniques in this workshop lend themselves well to sociological research, and the examples we will use come from a study on human behaviour, but they could easily be applied to observations of any system. For example, you might use an ordinal scale (e.g. 1-5, Disagree-Agree) to describe the condition of a plant seedling, with the question being something like "How wilted are the leaves, 1=no sign of damage, 5=leaves abcised". 

Firstly, we will learn how to format data from surveys and interviews effectively so that it can be easily used in analysis later. Knowing a few key data manipulation techniques will make processing the data much faster in the long run. Then we will explore various ways to visualise these data graphically, and finally we will run some simple statistical analyses to answer some hypotheses.

<b>Note : all the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-Qualit" target="_blank">this repository</a>. Clone and download the repo as a zip file, then unzip it.</b>

Alternatively, you can fork <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the repository</a> to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our <a href="https://ourcodingclub.github.io/2017/02/27/git.html" target="_blank">previous tutorial.</a>

## Getting Started

The first thing to do is open R Studio. Then make a new script file using `File/ New File/ R Script`, save it with a sensible name inside the folder you just downloaded and unzipped from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>.

Next, in your script file you need to set your working directory to the folder you just downloaded from <a href="https://github.com/ourcodingclub/CC-time-series" target="_blank">the github repository</a>. Copy and paste the code below as a guide, but remember that the path to your folder will be different:

```r
setwd("~/Downloads/CC-time-series-master")
```

Next, load (`library()`) the packages needed for this tutorial by running the code below in your script file. Remember to `install.packages()` if this is the first time you're using these packages:

```r
library(ggplot2)
library(dplyr)
```

Finally, load the data files we will be using for the tutorial.

```r

```

<DESCRIPTION of DATA>

## 1. Formatting qualitative data

<a name="format"></a>

Getting qualitative data into the right format for analysis can take some time. Most analytical tools are based on numerical values, so some coercion is needed to generate numerical values from our qualitative observations. In the case of a likert scale, this has already mostly been done for us. We have five discrete categories that follow an order from low to high, in this case <DESCRIPTION>. Even so, on our data sheet, whoever entered all the data has instead used the raw descriptors (e.g. <DESCRIPTION>), instead of their numerical equivalents (e.g. 4). This can be fixed with a tool called `gsub()`. `gsub()` finds strings that you search for in the data and replaces them with whatever you choose. In this case:

```r
<CODE>

```

The first argument of `gsub()` is the pattern to be replaced, the second is the replacement to be substituted in, and the third is the data to act on.

Depending on the question asked and what the responses show, responses from a likert scale are normally encoded from 1 to 5, or from -2 to +2


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

