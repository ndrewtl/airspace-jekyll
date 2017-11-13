---
layout: post
title: Quantifying and visualising population trends
subtitle: Making a map of vertebrate population change in Europe
date: 2017-11-11 21:11:27
author: Gergana
meta: "Tutorials"
tags: datavis
---
<div class="block">
          <center><img src="{{ site.baseurl }}/img/tutheaderEAB.png" alt="Img"></center>
        </div>



### Tutorial Aims:

#### <a href="#tidy"> 1.  Tidy dataset </a>

#### <a href="#calc"> 2. Calculate population change </a>

#### <a href="#map"> 3. Make a map of vertebrate population change in Europe </a>


### All the files needed to complete this tutorial can be downloaded from this <a href="https://github.com/ourcodingclub/CC-EAB" target="_blank">Github repository</a>. Click on `Clone or Download/Download ZIP` and then unzip the files.

__In this tutorial we will create a map showing the locations of vertebrate species populations from different orders and the direction in which those populations have changed in the last 60 years. We will use a dataset from the <a href="http://www.livingplanetindex.org/home/index" target="_blank">Living Planet Index Database</a>, which is publicly available. For the purpose of this tutorial, we have extracted a subset of the database (`LPI_EU.csv`) that includes vertebrate populations from the ten most common orders in Europe - _Passeriformes, Carnivora, Charadriiformes, Anseriformes, Falconiformes, Salmoniformes, Ciconiiformes, Artiodactyla, Perciformes, Cypriniformes_.__

Here is an example map, showing where the populations from the order Anseriformes were located, as well as how their populations have changed between 1950 and 2015. Looks like most of the populations have remained stable, with a slope around zero, three populations have increased, and a few have decreased. Here, we have demonstrated how to do the analysis on the population level, with a focus on how all species within a given order a changing, but you can filter the dataset if there is a particular species you are interested in.

<center><img src="{{ site.baseurl }}/img/anseriformes.png" alt="Img" style="width: 700px;"/>
<p><b>Figure 1. <i>Anseriformes</i> populations in Europe.</b></p></center>

Open RStudio and make a new script by clicking on `File/New File/R Script`. Usually we open RStudio on half of our screen, and the tutorial on the other half, as that way it's easy to copy code across and google errors if they arise.

<center><img src="{{ site.baseurl }}/img/workshop2.png" alt="Img" style="width: 700px;"/></center>

Headers and comments outline why we are taking the various steps in our analyses. Future you, your supervisors or collaborators will all benefit from informative comments. 

```r
# Aim of the script
# Your name and date

# Set working directory to where you saved the LPI EU data
setwd("D:/R/workshops/AEB")
# This is a sample filepath, it will be different on your laptop
# Alternatively, you can click on Session/Set Working Directory/Choose directory and navigate to your folder, but we recommend you still copy the code from the console to your script, so that future you knows from where the files came

# Load libraries ----
library(readr)
library(tidyr)
library(dplyr)
library(broom)
library(ggplot2)
library(ggthemes)
library(maps)
library(mapdata)
library(viridis)

# Load data ----
LPI_EU <- read_csv("AEB/LPI_EU.csv")
# Use read_csv not read.csv, so that the year columns are read in as characters
# They have an awkward "x" in front of the numbers, you'll see it later when we get rid of it

head(LPI_EU)
tail(LPI_EU)
str(LPI_EU)
View(LPI_EU)
```

The data are currently in wide format - each year is a column, which is not convenient for analysis. In a <a href="http://garrettgman.github.io/tidying/" target="_blank">"tidy"</a> dataset each row is an observation, so we can transform the dataset into long format using the `gather()` function from the `tidyr` package.

```r
# Transform data to long format ----
LPI_long <- gather(data = LPI_EU, key = "year", value = "population", select = 24:89)
# `select = 24:89` refers to the columns we want to gather, from the 24th to the 89th column

# Turn the year column into a numeric variable and get rid of the "x"
LPI_long$year <- parse_number(LPI_long$year)
str(LPI_long)  # population and year shouldn't be character variables
LPI_long$year <- as.numeric(as.character(LPI_long$year))
LPI_long$population <- as.numeric(as.character(LPI_long$population))
```

The <a href="http://www.livingplanetindex.org/home/index" target="_blank">Living Planet Index Database</a> contains records from hundreds of populations from 1950 to recent time, but the populations weren't surveyed every year, thus there are rows which say `NULL`. We can remove those rows, so that the `population` column contains only numeric values.

Since we will be calculating population change, to get more reliable estimates, we can conduct the analysis only using populations which have at least 5 records. Populations with only a few records might show a strong directional population change that is actually just noise in the data collection. We can also scale population size, so that the abundance of each species in each year is somewhere between 0 and 1. This helps when we are analysing many different populations whose numbers are very variable - e.g. some populations have 10-20 individuals, others have thousands.

```r
# Remove rows with no population information (population = NULL)
LPI_long <- filter(LPI_long, population != "NULL")

# Select only populations which have at least 5 data points
LPI_long <- LPI_long %>% group_by(id) %>% filter(length(unique(year)) > 4)

# Scale population size to be from 0 to 1
LPI_long$scalepop <- (LPI_long$population - min(LPI_long$population))/(max(LPI_long$population)-min(LPI_long$population))
```

<a name="calc"></a>
We have subsetted the data for the ten most common orders in the LPI European database, so we can quantify the change in populations from an order of our choice. Alternatively, we can calculate population change for all orders, or for just the marine or terrestrial ones, many options!

```r
# Calculate population change for an order of your choice ----
unique(LPI_long$order)  # displays all order options
anseriformes <- filter(LPI_long, order == "Anseriformes")
```

__We will use the `dplyr` and `broom` packages, which together create an efficient workflow in calculating population change. We will use linear models, from which we will extract the slope values - positive slopes indicate a population increase, negative slopes - a population decline, and a slope of zero indicates no net change.__

__Pipes, designated by the pipe operator `%>%`, are a way to streamline your analysis - imagine your data going in one end of a pipe, then you transform it, do some analysis on it, and then whatever comes out the other end of the pipe, gets saved in the object to which you are assigning the pipe.__ You can find a more detailed explanation of data manipulation using `dplyr` in our <a href="https://ourcodingclub.github.io/2017/01/16/piping.html" target="_blank">data formatting and manipulation tutorial</a>.

```r
pop_change <- anseriformes %>%
  group_by(latitude, longitude, binomial, id) %>%  # any column you want to keep, include here
  # the functions that follow will act on the last variable in the grouping
  # id represents a column with a unique number for each population
  # binomial is the species name
  do(mod = lm(scalepop ~ year, data = .)) %>%  # Create a linear model for each group
  # when using a non-dplyr function in a pipe, you have to put do() around it
  tidy(mod) %>%  # Extract model coefficients
  select(., latitude, longitude, binomial, id, term, estimate) %>%  # select the columns we want
  spread(., term, estimate) %>%  # transform them in a useful format
  ungroup()  # get rid of the grouping
```

<a name="map"></a>
We are now all set to make our map! This is a simple map we will make using `ggplot2`, it doesn't have topography, or cities and roads. Instead, it presents a stylised view of European countries and focuses on where the different populations are located and how they have changed.

We are using the `viridis` package for the colour palette of the points. The `viridis` package contains four colour palettes, which are friendly to colour blind people, and they look quite nice in general.

You can use the default `viridis` palette by just specifying `scale_colour_viridis()`, and if you want to try the other three options, you can instead use `scale_colour_viridis(option = "magma")`. The other two options are `inferno` and `plasma`.

```r
(EU_pop <- ggplot(pop_change, aes(x = longitude, y = latitude, fill = year)) +
    borders("world", xlim = c(-10, 25), ylim = c(40, 80), colour = "gray40", fill = "gray75", size = 0.3) +
    theme_map() +
    geom_point(shape = 21, colour = "black", alpha = 0.8, size = 4, position = position_jitter(w = 1.5, h = 1.5)) +
    # there are quite a few points, so we can use jittering to avoid overplotting
    scale_fill_viridis() +
    theme(legend.position = "right",
          legend.title = element_text(size = 16),
          legend.text = element_text(size = 12),
          legend.justification = "center",
          plot.title = element_text(size = 20, vjust = 1, hjust = 0.6, face = "italic")) +
    labs(colour = "Slope", title = "Anseriformes"))
```

__We can save our map using `ggsave()` from the `ggplot2` package, the default `width` and `height` are measured in inches. If you want to swap to pixels or centimeters, you can add `units = "px"` or `units = "cm"` inside the `ggsave()` brackets, e.g. `ggsave(object, filename = "mymap.png", width = 1000, height = 1000, units = "px"`.__

```r
ggsave(EU_pop, filename = "anseriformes.pdf", width = 10, height = 10)
ggsave(EU_pop, filename = "anseriformes.png", width = 10, height = 10)
```

<center><img src="{{ site.baseurl }}/img/anseriformes.png" alt="Img" style="width: 700px;"/>
<p><b>Figure 1. <i>Anseriformes</i> populations in Europe.</b></p></center>

Here we have created a map for _Anseriformes_, an order which includes many species of waterfowl, like the mallard and pochard. Curious to see how vertebrate populations across the whole LPI database have changed? You can check out our <a href="https://ourcodingclub.github.io/2017/03/20/seecc.html" target="_blank">tutorial on efficient ways to quantify population change</a>, where we compare how for-loops, `lapply()` functions and pipes compare when it comes to dealing with lots of data.

### We'd love to see the maps you've made, so feel free to email them to us at ourcodingclub@gmail.com!


<hr>
<hr>

<h3><a href="https://www.surveymonkey.co.uk/r/NYVBNF8" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
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
