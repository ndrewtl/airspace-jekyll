---
layout: post
title: Python Data Analysis with Pandas
subtitle: Using the Python data analysis package pandas
date: 2018-04-17 00:00:00
author: Declan V.
meta: "PythonPandas"
tags: python pandas
---
<div class="block">
  <center><img src="{{ site.baseurl }}/img/tutheader_python.png" alt="Img"></center>
</div>

### Tutorial aims:

#### <a href="#understanding"> Understand why Python is so useful for scientific programming</a>



<a name="understanding"></a>

## Understanding why Python is so useful for scientific programming


<center><img src="{{ site.baseurl }}/img/python_growth_major_languages.png" alt="Img" style="width: 1000px"></center>


If you are interested in reading more about the growth of Python (and the background to the above charts), I highly recommend reading <a href="https://stackoverflow.blog/2017/09/06/incredible-growth-python/" target="_blank">this blog post from StackOverflow</a>.


## Summary

In this tutorial we have looked at why Python is popular for scientific programming, and gotten a feel for how Python looks and feels. Hopefully, you have learnt some of the basic syntax, and how to write and run simple python scripts to read in data from text files, and make a simple plot of some of the data.

### Tutorial outcomes:

#### 1. You have a feel for how widely used Python is, and why it is popular

#### 2. You can run a simple test Python program on your computer

#### 3. You can read in data from a text file using the core Python language

#### 4. You can use modules and packages to streamline data reading and analysis

#### 5. You can make simple figures with matplotlib

#### 6. You have a feel for some of the basic syntax and data structures of Python


<hr>
<hr>

<h3><a href="https://www.surveymonkey.co.uk/r/WVL5GXB" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
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







