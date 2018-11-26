---
layout: post
title: Intro to the Google Earth Engine
subtitle: Quantifying forest cover change & harnessing the power of the Earth Engine to answer research questions
date: 2018-11-27 10:00:00
author: Gergana and Isla
meta: "Tutorials"
tags: modelling data_manip data_vis
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheaderdesign_to_be_added.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#intro"> 1. Learn what is the Google Earth Engine </a>
#### <a href="#analyses"> 2. Find out what types of analyses you can do using the GEE </a>
#### <a href="#layout"> 3. Get familiar with the GEE layout </a>
#### <a href="#javascript"> 4. Learn the basic principles of JavaScript </a>
#### <a href="#import"> 5. Import and explore data - forest cover change as a case study </a>
#### <a href="#visualise"> 6. Visualise forest cover change </a>
#### <a href="#calculate"> 7. Calculate forest cover change over time in specific locations</a>
#### <a href="#export"> 8. Export results - summary tables and geoTIFFs </a>
#### <a href="#R"> 9. Further analysis and visualisation in R - the best of both world! </a>

### All the files you need to complete this tutorial will be generated and exported from the GEE during the course of the tutorial.
## Introduction

__Ecological data can throw up complex challenges for statistical models and designing the appropriate model to answer your research question can be one of the trickiest parts of ecological research (and research in other fields). Learning how to design statistical models can take time, but developing rigorous statistical approaches as early as possible will help you in your future research career. If you put the time in, soon you will realise that statistics aren't a total pain and continuous frustration, but something pretty fun that really engages your brain in diverse ways. So to start off, I like to put the computer coding aside, to make my self a hot drink or get a fancy latte at a coffee shop, get out my pen or pencil and paper and put on my thinking cap.__

<a name="intro"></a>

## 1. Learn what is the Google Earth Engine

- Register

<a name="analyses"></a>

## 2. Find out what types of analyses you can do using the GEE


<a name="layout"></a>

## 3. Get familiar with the GEE layout


<center> <img src="{{ site.baseurl }}/img/graph.png" alt="Img" style="width: 400px;"/> </center>

<a name="javascript"></a>

## 4. Learn the basic principles of JavaScript


<a name="import"></a>

## 5. Import and explore data - forest cover change as a case study


<a name="visualise"></a>

## 6. Visualise forest cover change


<a name="calculate"></a>

## 7. Calculate forest cover change over time in specific locations


<a name="export"></a>

## 8. Export results - summary tables and geoTIFFs


<a name="R"></a>

## 9. Further analysis and visualisation in R - the best of both world!




<hr>
<hr>

__Check out <a href="https://ourcodingclub.github.io/workshop/" target="_blank">this page</a> to learn how you can get involved! We are very happy to have people use our tutorials and adapt them to their needs. We are also very keen to expand the content on the website, so feel free to get in touch if you'd like to write a tutorial!__

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/). <a href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://licensebuttons.net/l/by-sa/4.0/80x15.png" alt="Img" style="width: 100px;"/></a>

<h3><a href="https://www.surveymonkey.co.uk/r/PFJ7S2D" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>

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
