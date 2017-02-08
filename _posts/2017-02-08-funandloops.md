---
layout: post
title: Intro to loops and functions
subtitle: Saving yourself lots of copying and pasting
date: 2017-02-08 08:00:00
author: Gergana
meta: "Tutorials"
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheaderloop.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#function"> 1. Learn to write functions to code more efficiently</a>

#### <a href="#loop"> 2. Learn to write loops to make multiple graphs at once</a>

<a name="function"></a>

<b>Note : all the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-5-fun-and-loop">this repository</a>.</b>

### Writing functions

We've learned <a href="https://ourcodingclub.github.io/2016/11/13/intro-to-r.html">how to import our data in RStudio</a>, <a href="https://ourcodingclub.github.io/2017/01/16/piping.html">format and manipulate them</a>, <a href="https://ourcodingclub.github.io/2016/11/24/rmarkdown-1.html">write scripts and Markdown reports</a>, and <a href="https://ourcodingclub.github.io/2017/01/29/datavis.html">how to make beautiful and informative graphs using `ggplot2`</a>. When beautifying graphs, you might have noticed how you almost always repeat the same code - you always want to make the font size a bit bigger, get rid of the grey background in the default `ggplot2` theme, etc. When you are doing the same thing over and over again, it's useful to write it as a <b>function</b>. A function in R is a pre-determined command (or set of commands), for example `sum()` is a function that adds whatever is in the brackets, i.e. `sum(1+2)` will return a value of `3`. R has lots of functions built in within the `base` package R comes with, and you've been using heaps more from within all the other packages you've been installing. But you can also write your own functions to save yourself time from copying and pasting and making your coding more  efficient.

Open RStudio, select `File/New File/R script` and start writing your script with the help of this tutorial.

```r
# Purpose of the script
# Your name, date and email

# Libraries - if you haven't installed them before, run the code install.packages("package_name")
library(dplyr)
library(ggplot2)
library(gridExtra)
```

We will use data from the <a href="http://www.livingplanetindex.org/home/index">Living Planet Index</a>, which you have already downloaded from <a href="https://github.com/ourcodingclub/CC-5-fun-and-loop">the repository</a> (Click on 'Clone or Download/Download ZIP' and then unzip the files). When you run the `read.csv(file.choose())` code, a window will pop up, from where you can navigate to the folder where you saved the `LPI_data_loops.csv` file. Note that this is a different subset of the LPI data and not the same as in the <a href="https://ourcodingclub.github.io/2017/01/29/datavis.html">data visualisation tutorial</a>, so please download the new data file from <a href="https://github.com/ourcodingclub/CC-5-fun-and-loop">here</a>.

```r
# Import data from the Living Planet Index - population trends of vertebrate species from 1970 to 2014
LPI <- read.csv(file.choose())
```

<b> You might remember making this scatter plot from the data visualisation tutorial, let's go through it again for some `ggplot2` practice, and to set the scene for our functions later.

#### Scatter plot to examine how Griffon vulture populations have changed between 1970 and 2017 in Croatia and Italy

```r
vulture <- filter(LPI_data_loops, Common.Name == "Griffon vulture / Eurasian griffon")
vultureITCR <- filter(vulture, Country.list == c("Croatia", "Italy"))

(vulture_scatter <- ggplot(vultureITCR, aes (x=year, y=abundance, colour=Country.list)) +
    geom_point(size=2) +                                                # Changing point size
    geom_smooth(method=lm, aes(fill=Country.list)) +                    # Adding a linear model fit and colour-coding by country
    scale_fill_manual(values = c("#EE7600", "#00868B")) +               # Adding custom colours
    scale_colour_manual(values = c("#EE7600", "#00868B"),               # Adding custom colours
                        labels=c("Croatia", "Italy")) +                 # Adding labels for the legend
    ylab("Griffon vulture abundance\n") +                             
    xlab("\nYear")  +
		theme_bw() +
    theme(axis.text.x=element_text(size=12, angle=45, vjust=1, hjust=1),       # making the years at a bit of an angle
          axis.text.y=element_text(size=12),
          axis.title.x=element_text(size=14, face="plain"),             
          axis.title.y=element_text(size=14, face="plain"),             
          panel.grid.major.x=element_blank(),                                  # Removing the background grid lines                
          panel.grid.minor.x=element_blank(),
          panel.grid.minor.y=element_blank(),
          panel.grid.major.y=element_blank(),  
          plot.margin = unit(c(0.5, 0.5, 0.5, 0.5), units = , "cm"),           # Adding a 0.5cm margin around the plot
          legend.text = element_text(size=12, face="italic"),                  # Setting the font for the legend text
          legend.title = element_blank(),                                      # Removing the legend title
          legend.position=c(0.9, 0.9)))               # Setting the position for the legend - 0 is left/bottom, 1 is top/right
```

<b>Here we are using the `theme_bw()` theme but we are making lots of modifications to it. We tend to make the same modifications to it, so lets turn them into a function! To start writing a function, you first designate an object to it - what will your function be called? Since we are making a personalised theme for `ggplot2`, here I've called my function `theme_my_own`. To tell R that you are writing a function, you use `function()` and then in the commands that you want your function to include go between the `{}`.</b>

```r
theme_my_own <- function(){
  theme_bw()+
  theme(axis.text.x=element_text(size=12, angle=45, vjust=1, hjust=1),
        axis.text.y=element_text(size=12),
        axis.title.x=element_text(size=14, face="plain"),             
        axis.title.y=element_text(size=14, face="plain"),             
        panel.grid.major.x=element_blank(),                                          
        panel.grid.minor.x=element_blank(),
        panel.grid.minor.y=element_blank(),
        panel.grid.major.y=element_blank(),  
        plot.margin = unit(c(0.5, 0.5, 0.5, 0.5), units = , "cm"),
        plot.title = element_text(size=20, vjust=1, hjust=0.5),
        legend.text = element_text(size=12, face="italic"),          
        legend.title = element_blank(),                              
        legend.position=c(0.9, 0.9))
}
```

<img src="{{ site.baseurl }}/img/gg_scatter3.png" alt="Img" style="width: 600px;"/>
Figure 1. Population trends of Griffon vulture in Croatia and Italy from 1970 to 2014. 
Data points represent raw data with a linear model fit and 95% confidence intervals.

<b>Now we can make the same plot, but this time instead of all the code, we can just add `+ theme_my_own()`. Try changing the colours we use in the plot - where it says `"#EE7600", "#00868B"`, you need to add in the code for colours of your choice. TIP: Check out our <a href="">data visualisation tutorial</a> that includes instructions on how to install Colourpicker - Colourpicker is an addin for RStudio that saves you time from googling colour codes.</b>

```r
(vulture_scatter <- ggplot(vultureITCR, aes (x=year, y=abundance, colour=Country.list)) +
    geom_point(size=2) +                                                
    geom_smooth(method=lm, aes(fill=Country.list)) +                    
    theme_my_own() +                                                    # Adding our new theme!
    scale_fill_manual(values = c("#EE7600", "#00868B")) +               
    scale_colour_manual(values = c("#EE7600", "#00868B"),               
                        labels=c("Croatia", "Italy")) +                 
    ylab("Griffon vulture abundance\n") +                             
    xlab("\nYear"))
```


#### Let's make more plots, again using our customised theme

<b>Filter the data to include only UK populations.</b>

```r
LPI.UK <- filter(LPI_data_loops, Country.list == "United Kingdom")

# Pick 4 species and make scatterplots with linear model fits that show how the population has varied through time
# Careful with the spelling of the names, needs to match the name of the species in the LPI.UK dataframe

house.sparrow <- filter(LPI.UK, Common.Name == "House sparrow")
great.tit <- filter(LPI.UK, Common.Name == "Great tit")
corn.bunting <- filter(LPI.UK, Common.Name == "Corn bunting")
reed.bunting <- filter(LPI.UK, Common.Name == "Reed bunting")
meadow.pipit <- filter(LPI.UK, Common.Name == "Meadow pipit")
```


#### Making the plots

```r
(house.sparrow_scatter <- ggplot(house.sparrow, aes (x=year, y=abundance)) +
    geom_point(size=2, colour="#00868B") +                                                
    geom_smooth(method=lm, colour="#00868B", fill="#00868B") +          
    theme_my_own() +
    labs(y = "Abundance\n", x="", title="House sparrow"))

(great.tit_scatter <- ggplot(great.tit, aes (x=year, y=abundance)) +
    geom_point(size=2, colour="#00868B") +                                                
    geom_smooth(method=lm, colour="#00868B", fill="#00868B") +          
    theme_my_own() +
    labs(y = "Abundance\n", x="", title="Great tit"))

(corn.bunting_scatter <- ggplot(corn.bunting, aes (x=year, y=abundance)) +
    geom_point(size=2, colour="#00868B") +                                                
    geom_smooth(method=lm, colour="#00868B", fill="#00868B") +          
    theme_my_own() +
    labs(y = "Abundance\n", x="", title="Corn bunting"))

(meadow.pipit_scatter <- ggplot(meadow.pipit, aes (x=year, y=abundance)) +
    geom_point(size=2, colour="#00868B") +                                                
    geom_smooth(method=lm, colour="#00868B", fill="#00868B") +          
    theme_my_own() +
    labs(y = "Abundance\n", x="", title="Meadow pipit"))
```

#### Now arrange all 4 plots in a panel and save the file

```r
panel <- grid.arrange(house.sparrow_scatter, great.tit_scatter, corn.bunting_scatter, meadow.pipit_scatter, ncol=2)
ggsave(panel, file="Pop_trend_panel.png", width=10, height=8)
```

<center><img src="{{ site.baseurl }}/img/Pop_trend_panel.png" alt="Img" style="width: 1000px;"/>
Figure 1. Population trends of four bird species from 1970 to 2014 based on the Living Planet Index database. Data points represent raw data with a linear model fit and 95% confidence intervals.</center>

<a name="loop"></a>

### Loops

That wasn't too bad, but you are still repeating lots of code, and here you have only 4 graphs to make - what if you had to make a graph like this for every species in the `LPI.UK` dataset? That would mean repeating the same code over 200 times. That will be very time consumming, and it's very easy to make mistakes when you are monotonously copying and pasting for hours.

<b> You might be noticing a pattern in what we have been doing - for every species, we want R to make the same type of graph. We can tell R to do exactly that using a loop! Loops are used for iterative actions, i.e. when for every species/year/some variable in your dataset, you want R to apply the same set of functions to it.</b>.

<b>First we need to make a list of species - we will tell R to make a graph for every item in our list.</b>

```r
Sp_list <- list(house.sparrow, great.tit, corn.bunting, meadow.pipit)
```

# Writing the loop

```r
for (i in 1:length(Sp_list)) {                                    # For every item along the length of Sp_list we want R to perform the following functions
  data <- as.data.frame(Sp_list[i])                               # Create a dataframe for each species
  sp.name <- unique(data$Common.Name)                             # Create an object that holds the species name, so that we can title each graph
  plot <- ggplot(data, aes (x=year, y=abundance)) +               # Make the plots and add our customised theme
    geom_point(size=2, colour="#00868B") +                                                
    geom_smooth(method=lm, colour="#00868B", fill="#00868B") +          
    theme_my_own() +
    labs(y = "Abundance\n", x="", title = sp.name)

  ggsave(plot, file=paste(sp.name, ".pdf", sep=''), scale=2)       # save plots as .pdf, you can change it to .png if you prefer that

  print(plot)                                                      # print plots to screen
}
```

The files will be saved in your working directory - to find out where that is, run the code `getwd()` and to set a new working directory, run the code `setwd("Insert file path here")`, or click `Session/Set Working directory/Choose Working Directory` from the RStudio menu.

You can now write functions and loops - congrats! Feel free to contact us with any questions at ourcodingclub@gmail.com.
