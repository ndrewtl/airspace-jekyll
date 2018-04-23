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

Welcome to this tutorial about doing data analysis with `pandas`. If you did the Introductory Python tutorial, you'll rememember we briefly looked at the `pandas` package as a way of quickly loading a .csv file to extract some data. This tutorial looks at pandas in some more depth. 

### Tutorial aims:

#### <a href="#understanding">Understand what Pandas is</a>

#### <a href="#following">Ways of running Python and Pandas</a>

<a name="understanding"></a>

## What is pandas?

Pandas is a package commonly used to deal with data analysis. It simplifies the loading of data from external sources such as text files and databases, as well as providing ways of analysing and manipulating data once it is loaded into your computer. The features provided in pandas automate and simplify a lot of the commonly used tasks that would take many lines of code to write in the basic Python langauge.

_If you have used R's dataframes before, or the NumPy package in Python, you may find some similarities in the Python `pandas` package. But if not, don't worry because this tutorial doesn't assume any knowledge of NumPy or R, only basic-level Python._

Pandas is a hugely popular, and still growing, Python library used across a range of disciplines from environmental and climate science, through to social science, linguistics, biology, as well as a number of applications in industry such as data analytics, financial trading and many others. If you came to the last tutorial, you'll know I'm a fan of these StackOverflow graphs showing usage of programming languages over time. Well here is another one showing the growth of Pandas compared to some other Python software libraries! (Based on StackOverflow question views per month).

<center><img src="{{ site.baseurl }}/img/python_pandas_growth.png" alt="Img" style="width: 1000px"></center>

These graphs of course should be taken with a pinch of salt, as there is no agreed way of absolutely determing programming langauge and library popularity, but they are interesting to think about nonetheless. 

Pandas is best suited for structured, __labled__ data, in other words, tabular data, that has headings or names associated with each column of data. The pandas.org website describes its data-handling strengths as:

##### Tabular data with heterogeneously-typed columns, as in an SQL table or Excel spreadsheet
##### Ordered and unordered (not necessarily fixed-frequency) time series data.
##### Arbitrary matrix data (homogeneously typed or heterogeneous) with row and column labels
##### Any other form of observational / statistical data sets. The data actually need not be labeled at all to be placed into a pandas data structure
 
Some other important points to note about pandas are:

##### pandas is __fast__. Python sometimes gets a bad rap for being a bit slow compared to 'compiled' languages such as C and Fortran. But deep down in the internals of Pandas, it is actually written in C, and so processing large datasets is no problem for pandas.
##### pandas is a dependency of another library called `statsmodels`, making it an important part of the statistical computing ecosystem in Python.

You can read more about the pandas package at the <a href="https://pandas.pydata.org/" target="_blank">pandas project website</a>.

## Following this tutorial

### Spyder

If you are attending the workshop 'live' on-site at Edinburgh University, the easiest way is to use the Spyder IDE (Integrated Development Environment) which is installed on the university computers. It can also be installed on your laptop relatively easily. It is included in the <a href="https://www.anaconda.com/download/" target=_"blank">Anconda Python distibution which can be downloaded here</a>. Be sure to download the Python 3 version!

The basics of Spyder were covered in the Introduction to Python workshop.

### Terminal or Command-line

You can follow this tutorial by writing scripts saved as `.py` files and then running the script from the terminal or command line with the `python` command. e.g.

```bash
python myscript.py
```

### Interactively with iPython

IPython is an 'interactive' python interpreter. It lets you type in Python command line-by-line, and then immediately executes them. It's a very useful way of quickly testing and exploring python commands, because you don't have to interact directly with the command line or run the entire script. Spyder has an IPython console built in to it (on the right hand panel), or it can be started from the command line by running:

```bash
ipython
```


## Summary

In this tutorial we have looked at why pandas...

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







