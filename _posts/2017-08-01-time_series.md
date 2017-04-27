---
title: "Analysing time series data"
author: "John"
date: "2017-03-20 10:00:00"
meta: Tutorials
subtitle: "Quantifying ..."
layout: post
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheadertimeseries.png" alt="Img">
	</center>
</div>


### Tutorial Aims:

#### <a href="#format"> 1. Formatting time series data </a>

#### <a href="#"> 2. </a>

#### <a href="#datavis"> 3. Visualising time series analysis</a>

#### <a href="#stats"> 4. Statistically analysing time series data</a>

# INTRO TITLE

<center><img src="{{ site.baseurl }}/img/tidyverse.png" alt="Img" style="width: 1100px;"/></center>

All the resources for this tutorial, including some helpful cheatsheets can be downloaded from [this repository](https://github.com/ourcodingclub/SEECC-workshop) Clone and download the repo as a zipfile, then unzip and set the folder as your working directory by running the code below (subbing in the actual folder path), or clicking `Session/ Set Working Directory/ Choose Directory` from the RStudio menu.

Alternatively, you can fork [the repository](https://github.com/ourcodingclub/SEECC-workshop) to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our previous <a href="https://ourcodingclub.github.io/2017/02/27/git.html">tutorial.</a>

Make a new script file using `File/ New File/ R Script` and we are all set to explore how biodiversity has changed based on the LPI data.

```r
setwd("PATH_TO_FOLDER")
```

Next, install (`install.packages("")`) and load (`library()`) the packages needed for this tutorial.

```r
install.packages("readr")

library(RColorBrewer)
```

Finally, load the `.RData` files we will be using for the tutorial.

```r
load("")
```

<a name="format"></a>

## 1. Formatting time series data 

__INSERT BODY__


<hr>
<hr>

#### Check out our <a href="https://ourcodingclub.github.io/links/">Useful links</a> page where you can find loads of guides and cheatsheets.

#### If you have any questions about completing this tutorial, please contact us on ourcodingclub@gmail.com

#### <a href="SURVEY_MONKEY_LINK">We would love to hear your feedback on the tutorial, whether you did it in the classroom or online!</a>

<ul class="social-icons">
	<li>
		<h3>
			<a href="https://twitter.com/our_codingclub">&nbsp;Follow our coding adventures on Twitter! <i class="fa fa-twitter"></i></a>
		</h3>
	</li>
</ul>

### &nbsp;&nbsp;Subscribe to our mailing list:
<div class="container">
	<div class="block">
        <!-- subscribe form start -->
		<div class="form-group">
			<form action="https://getsimpleform.com/messages?form_api_token=de1ba2f2f947822946fb6e835437ec78" method="post">
			<div class="form-group">
				<input type='text' class="form-control" name='Email' placeholder="Email">
			</div>
			<div>
                        	<button class="btn btn-default" type='submit'>Subscribe</button>
                    	</div>
                	</form>
		</div>
	</div>
</div>
