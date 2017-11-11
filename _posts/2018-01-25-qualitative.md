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

#### <a href="#ggplot"> 1. Learn how to format survey data, coding responses </a>

#### <a href="#practice"> 2. Practice visualising ordinal data, count data, likert scales </a>

#### <a href="#panel"> 3. Statistically analyse qualitative data</a>

<a name="ggplot"></a>

<b>Note : all the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-Qualitative" target="_blank">this repository</a>. Clone and download the repo as a zip file, then unzip it.</b>

We've learned <a href="https://ourcodingclub.github.io/2016/11/13/intro-to-r.html" target="_blank">how to import our data in RStudio</a>, <a href="https://ourcodingclub.github.io/2017/01/16/piping.html" target="_blank">format and manipulate them</a>, and now it's time we talk about communicating the results of our analyses - data visualisation! When it comes to data visualisation, the package `ggplot2` by Hadley Wickham has won over many scientists' hearts. In this tutorial, we will learn how to make beautiful and informative graphs and how to arrange them in a panel. Before we take on the `ggplot2` syntax, let's briefly cover what good graphs have in common.


<BODY>

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

