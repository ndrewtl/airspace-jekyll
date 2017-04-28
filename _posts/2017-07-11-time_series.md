---
title: "Analysing time series data"
author: "John"
date: "2017-07-11 10:00:00"
meta: Tutorials
subtitle: "Exploring "
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

#### <a href="#datavis"> 3. Visualising time series data</a>

#### <a href="#stats"> 4. Statistically analysing time series data</a>

# INTRO TITLE

All the resources for this tutorial, including some helpful cheatsheets can be downloaded from [this repository](https://github.com/ourcodingclub/SEECC-workshop) Clone and download the repo as a zipfile, then unzip and set the folder as your working directory by running the code below (subbing in the actual folder path), or clicking `Session/ Set Working Directory/ Choose Directory` from the RStudio menu.

Alternatively, you can fork [the repository](https://github.com/ourcodingclub/SEECC-workshop) to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our previous <a href="https://ourcodingclub.github.io/2017/02/27/git.html">tutorial.</a>

Make a new script file using `File/ New File/ R Script` and we are all set to explore how biodiversity has changed based on the LPI data.

```r
setwd("PATH_TO_FOLDER")
```

Next, install (`install.packages("")`) and load (`library()`) the packages needed for this tutorial.

```r
install.packages("ggplot2")
install.packages("lubridate")
install.packages("scales")

library(ggplot2)
library(lubridate)
library(scales)
```

Finally, load the `.RData` files we will be using for the tutorial.

```r
load("")
```

<a name="format"></a>

## 1. Formatting time series data 

The most common issue with using time series data in R is getting it into the right format that is easily readable by R and any packages you are using. A sensible format for recording time series data to be readable by most computer programs presents the largest chunk of time first (e.g. year), and gets progressively smaller, e.g.:

```r
2017-02-25
```



If you can record your data in this format to begin with, things will be much easier. Obviously if time isn't important for your measurements, you can drop that part from your records.

The data in __ is currently interpreted by R as being from the `character` class. But R also has a `Date` class, which is much easier to work with, so we can coerce the data to the `Date` class:

```r
# Check the class of milk$Month
milk$Month_date_test <- as.Date(milk$Month, format = "%Y-%m-%d")

# Coerce to `Date` class
milk$Month_date <- as.Date(milk$Month)

# Check it worked
class(milk$Month_date) 
```

`format` lets `as.Date` know what form our time data was in. The symbols `%Y`, `%m`, `%d` etc. are codes understood by many programming languages to define date types, here is an expanded table of date codes:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-031e">Name</th>
    <th class="tg-031e">Code</th>
    <th class="tg-yw4l">Example</th>
  </tr>
  <tr>
    <td class="tg-031e">Long year</td>
    <td class="tg-031e">%Y</td>
    <td class="tg-yw4l">2017</td>
  </tr> 
  <tr>
    <th class="tg-031e">Short year</th>
    <th class="tg-031e">%y</th>
    <th class="tg-yw4l">17</th>
 <tr>
    <th class="tg-031e">Numeric month</th>
    <th class="tg-031e">%m</th>
    <th class="tg-yw4l">02</th>
  </tr> 
  <tr>
    <th class="tg-031e">Abbreviated month</th>
    <th class="tg-031e">%b</th>
    <th class="tg-yw4l">Feb</th>
  </tr> 
  <tr>
    <th class="tg-031e">Full month</th>
    <th class="tg-031e">%B</th>
    <th class="tg-yw4l">February</th>
  </tr> 
  <tr>
    <th class="tg-031e">Day</th>
    <th class="tg-031e">%d</th>
    <th class="tg-yw4l">25</th>
  </tr>
  <tr>
    <th class="tg-031e">Abbreviated weekday</th>
    <th class="tg-031e">%a</th>
    <th class="tg-yw4l">Sat</th>
  </tr> 
  <tr>
    <th class="tg-031e">Full weekday</th>
    <th class="tg-031e">%A</th>
    <th class="tg-yw4l">Saturday</th>
  </tr>  
  <tr>
    <th class="tg-031e">Day of the week (1-7)</th>
    <th class="tg-031e">%u</th>
    <th class="tg-yw4l">6</th>
  </tr>
  <tr>
    <th class="tg-031e">Day of the year</th>
    <th class="tg-031e">%j</th>
    <th class="tg-yw4l">56</th>
  </tr>
<\table>


<a name="datavis"></a>

## 3. Plotting time series data 

Plotting time series data with ggplot requires the use of `scale_x_date` to correctly build axis labels and allow easy customisation of axis ticks:

```r
ggplot(milk, aes(x = Month_date, y = milk_prod)) + 
	geom_line() + 
	scale_x_date(date_labels = "%Y", date_breaks = "1 year")
```

Play around with `date_labels`, replacing `"%Y"` with some other date marks from <a href="#date_marks">the table above</a> (i.e. `%m-%Y`). `date_breaks` can also be customised to change the axis label frequency, other options include `month`, `week` and `day`.

<a name="stats"></a>

## 4. Statistical analysis of time series data 

#### Decomposition
Time series data can contain multiple patterns at different scales. Have a look at a simple plot of `milk` like the one we saw earlier:

```r
ggplot(milk, aes(x = Month_date, y = milk_prod)) + 
	geom_line() + 
	scale_x_date(date_labels = "%Y", date_breaks = "1 year")
```

Firstly, it looks like there is a general upward trend, more milk is being produced in 1975 than in 1962. This is known as a "__smooth__" pattern, one that increases regularly over the course of the time series. We can see this pattern more clearly by plotting a loess regression through our data:

```r
ggplot(milk, aes(x = Month_date, y = milk_prod)) + 
	geom_smooth(method = "loess", se = FALSE, span = 0.6)
```

`span` sets the number of points used to plot each local regression in the curve, the smaller the number the more points are used and the more closely the curve will fit the original data.

Next, it looks like there are some peaks and troughs that occur within the same month in each year. This is a "__seasonal__" pattern. We can investigate this pattern more by plotting each year as it's own line and comparing:

```r
# Extract month and year and store in new column
milk$year <- format(milk$Month_date, "%Y")
milk$month_num <- format(milk$Month_date, "%m")

ggplot(milk, aes(x = month_num, y = milk_prod, group = year)) + 
	geom_line(aes(colour = year))
```

"__Cyclic__" trends are similar to seasonal trends in that they recur over time, but occur on longer time scales. It may be that the general upward trend we saw earlier may be part of a longer decadal cycle, but this is impossible to test without a longer time series.

#### Forecasting

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
