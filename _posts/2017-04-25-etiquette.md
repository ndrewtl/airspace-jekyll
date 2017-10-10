---
title: "Coding etiquette"
author: "Gergana"
date: "2017-04-25 08:00:00"
meta: Tutorials
subtitle: Writing clear, informative and easy to use code
layout: post
tags: intro_to_r, github, data_manip
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheaderet.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#sections"> 1. Organising scripts into sections </a>

#### <a href="#syntax"> 2. Following a coding syntax etiquette</a>

#### <a href="#tidy"> 3. Tidying up old scripts and data frames</a>

When analysing data in `R`, the lines of code can quickly pile up - hundreds of lines to scroll through, numerous objects whose names might make sense to you, but not to other people or future you. This tutorial offers tips on how to make your code easy to read, understand and use for yourself and others who may want to read your code in the future. Following a coding etiquette (a set of "rules" you follow consistently throughout your work) will improve your `R` workflow, and reduce errors arising from accidental overwriting of objects, typos when referring to objects, and similar small issues that might end up causing big frustrations.

The coding etiquette outlined in this tutorial is applicable to most analyses - here we will apply them to an analysis of vertebrate population change from a previous Coding Club tutorial on <a href="https://ourcodingclub.github.io/2017/01/29/datavis.html" target="_blank">Data Visualisation.</a> Alternatively, feel free to edit some of your own scripts following the coding etiquette guidelines below. 

### You can download all the resources for the tutorial, including some helpful cheatsheets from <a href="https://github.com/ourcodingclub/CC-4-Datavis" target="_blank">this repository.</a> Clone and download the repo as a zipfile, then unzip and set the folder as your working directory with code, or click `Session/ Set Working Directory/ Choose Directory` from the RStudio menu.

Alternatively, you can fork [the repository](https://github.com/ourcodingclub/CC-4-Datavis) to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our previous <a href="https://ourcodingclub.github.io/2017/02/27/git.html" target="_blank">tutorial.</a>

__You can copy across code from this tutorial into a blank script file for practice, or you can edit some of your own scripts.__

<a name="sections"></a>

### 1. Organising scripts into sections

As with any piece of writing, it really helps to have a clear structure to your script. A script is a `.R` file that contains your code - you could directly type code into the R console, but that way you have no record of it, and you won't be able to reuse it later. To make a new `.R` file, open RStudio and go to `File/New file/R script`. For more information on the general RStudio layout, you can check out our <a href="https://ourcodingclub.github.io/2016/11/13/intro-to-r.html" target="_blank">Intro to RStudio tutorial</a>. A clearly structured script allows both the writer and the reader to easily navigate through the code to find the desired section. 

`RStudio` has a very useful feature allowing you to see an outline of your script, similar to when using `Microsoft Word`. Now that you have made a new (blank) script file, you might notice a little outline icon in the top right corner of the script. If you click on it, you will see your outline - currently it is blank since we haven't added any code, but once we start creating sections, you will see them appear here. You can then click on the section you wish to view, and you are automatically taken to that part of the script. No more endless scrolling! __NOTE: If you don't see the outline icon, you most likely do not have the newest version of RStudio - if you want to get this feature, please update.__

<center> <img src="{{ site.baseurl }}/img/outline.png" alt="Img" style="width: 800px;"/> </center>

To create sections, first you need to add a comment using the `#` symbol. Comments are incredibly useful for making sense of code and clarifying what you are doing, and why you are doing it. Once you have a comment statement, like `# Testing comments`, you can add four or more `#` or `-` to make that comment the start of a section (e.g. `# Testing comments ----`). In your outline you will see this comment as your first section.

#### Script structure:

__There are no strict rules and you can adapt the number and names of sections to your needs, but in general a script includes the following sections:__

__Introductory section__ - Author statement (what does this script do?), author(s) names, contact details and date.

__Libraries__ - Ahat packages are you using for this script? Keep all of them together at the start of your script. When switching between scripts, with your packages already loaded, it's easy to forget to copy across the library, which means future you might get confused as to why the code isn't working anymore. Your library will be extra informative to you and other people if you add in comments about what you are using each package for.

__Here are two examples, good and bad, to illustrate these first two sections.__

__A not particularly useful script intro:__

```r
# My analysis
```

__A more informative script intro:__

```r
# Analysing vertebrate population change based on the Living Planet Index
# Data available from http://www.livingplanetindex.org/

# Gergana Daskalova ourcodingclub@gmail.com
# 25-04-2017

# Libraries ----
library(tidyr)  # Formatting data for analysis
library(dplyr)  # Manipulating data
library(ggplot2)  # Visualising results
```

__Functions__ - Are you using any functions written by you and/or others? Define them here. For example functions to remove `NA` values, functions to <a href="https://ourcodingclub.github.io/2017/02/08/funandloops.html" target="_blank">create your own `ggplot2` theme.</a>

```r
# Defining functions ----
# A custom ggplot2 function
theme_LPI <- function(){
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

__Setting the working directory__ - It helps to keep all your data, scripts, image outputs etc. in a single folder. This minimises the chance of losing any part of your analysis and makes it easier to move the analysis on your computer without breaking filepaths. Note that filepaths are defined differently on Mac/Linux and Windows machines. On a Mac/Linux machine, user files are found in the 'home' directory (`~`), whereas on a Windows machine files can be placed in multiple 'drives' (e.g. `D:`). Also note that on a Windows machine, if you copy and paste a filepath from Windows Explorer into RStudio, it will appear with backslashes (`\ `), but R requires all filepaths to be written using forward-slashes (`/`), so you will have to change those manually. See below for some examples of how to set the working directory for both Windows and Mac/Linux:

```r
# Set the working directory on Windows ----
setwd("D:/Work/LPI_analysis")

# Set the working directory on Mac/Linux ----
setwd("~/Work/LPI_analysis")
```

__Loading data__ - what data are you using and where is it stored?  An example section where data is loaded:

```r
# Load data ----
load("LPIdata_Feb2016.RData")
# Here we are using `load()` and RData files because the dataset is very big
# RData files are more compressed than `.csv` files
# Alternatively, here you can add your own .csv file using `read.csv("your_filepath")`
```

__The different sections of your analysis__ - what is the logical workflow of your analysis? Keep the order in which you tackle your analysis consistent. If this is code for an undergraduate dissertation, a thesis chapter, or a manuscript, you can follow the same order in your script. Here is an example - if you copy these across to a script file, you'll see the sections appear.

```r
# Formatting data ----
# Here you would add all your code for the formatting of your data, e.g.:
LPI2 <- gather(LPI, "year", "abundance", 9:53)  # Transforming the data from wide to long format
LPI2$year <- parse_number(LPI2$year)  # Do you see awkward Xs before all the years? This gets rid of them.
names(LPI2)  # Check what the different variables are called
names(LPI2) <- tolower(names(LPI2))  # Make all variable names lower case

# When manipulating data it's always good check if the variables have stayed how we want them
# Use the str() function
str(LPI2)

# Abundance is a character variable, when it should be numeric, let's fix that
LPI2$abundance <- as.numeric(LPI2$abundance)

# Calculating summary statistics ----
# Calculating summary statistics for each biome in the Living Planet Index database
LPI_biome_summ <- LPI2 %>%
  group_by(biome) %>%  # Group by biome
  summarise(populations = n(),   # Create columns, number of populations
            mean_study_length_years = mean(lengthyear),  # mean study length
            dominant_sampling_method = names(which.max(table(sampling.method))),  # modal sampling method
            dominant_units = names(which.max(table(units))))  # modal unit type

# Visualising the number of populations in each biome ---- 
```

__The outputs of your analysis__ - Remember to keep your filepath sensible not only when loading data in, but also when you are outputting files (e.g. `.Rdata`, `.csv` files and any figures you want saved). `.csv` files are more transferable and can be used across multiple platforms, whereas `.Rdata` files are more compressed and are quicker to work with. Saving graphs as `.pdf` files is better practice, since `.pdf` files are vector based and don't decrease in quality when you zoom in or out. `.png` files, on the other hand, are easily inserted in text documents and presentations, so ideally you should save a `.pdf` and a `.png` file of your graph. It is also good practice to save image outputs in a subdirectory of your working directory, e.g. `img/`:

```r
png(file="img/filename.png", width = 1000, height = 2000)  # Note that png() uses pixel values for width and height
# The code for your graph goes here
dev.off()  # This tells R you are done with the plotting and it can save the file

pdf(file="img/filename.png",  width = 13.33, height = 26.66)  # pdf() uses inches
# The code for your graph goes here
dev.off()
```

__You might have noticed that when you create a section using four or more `#` or `-` at the end of a comment line, a little arrow appears in front of the comment. Another very useful feature of R Studio is that you can collapse and expand sections. This becomes especially useful when traversing a long script, just collapse the unwanted sections. If there is something you want to check out in the collapsed section, you can click the little arrow again to expand it.__

<center> <img src="{{ site.baseurl }}/img/outline4.png" alt="Img" style="width: 800px;"/> </center>

__You can also go to `Edit/Folding/Collapse all` to collapse all sections - this is the outline of your script, and from here you can navigate to whichever section you need. `Expand all` displays all of the code you've written. Here is an example:__

<center> <img src="{{ site.baseurl }}/img/outline2.png" alt="Img" style="width: 800px;"/> </center>

<a name="syntax"></a>


### 2. Following a coding syntax etiquette

#### 2.1. Naming files and objects.

#### "There are only two hard things in Computer Science: cache invalidation and naming things." - Phil Karlton

We're not too familiar with cache invalidation, but we would definitely agree that naming things is hard, and going for a quick and easy solution, like calling your graphs `graph`, might cause trouble later!

__File names for scripts should be meaningful and end in `.R`. Avoid spaces and funky characters!!! They can cause trouble when uploading files to Github and in general when trying to locate files through certain file paths.__

```r
LPI_analysis_Apr_2017.R  # Alright.

yet_another_script.R  # Bad. Took me hours to find the file when I needed it one year later.
```

__Object names should be concise and meaningful.__

Calling your data `data` might cause problems if you are doing multiple analyses at once / don't clean your environment, and you keep using the same object name. But if you need an overwrittable universal object and you don't need to keep lots of objects from each step of your analysis, sticking with the same object name might be useful.

Long object names are annoying to type - more letters = higher chance you'll make a typo.

Variable and function names should be lowercase. `MinPrecip_august` is confusing to remember, `min.precip.aug` is a bit long, but informative and easier to type.

##### - __Variable names should be nouns.__ E.g. `abundance` `richness`
##### - __Function names should be verbs.__ E.g. `calc.sp.richness`
##### - __Use an underscore to separate words within a script file.__ E.g. `LPI_analysis_Apr_2017.R`
##### - __Use a dot to separate words within objects and functions.__ E.g. `pop.change.m` for the object that stores a model examining population change, and `calc.sp.richness` for a function.
##### - __The preferred form for variable names is all lower case letters and words separated with dots (`variable.name`).__

#### Note that <a href="http://adv-r.had.co.nz/Style.html ">Hadley Wickham's style guide</a> advises to use underscores to separate words within objects, e.g. `variable_name`.

As pointed out by one of our readers, using dots to separate words in objects names has the potential to get confused with method dispatch mechanism.

__This way it's clear what's an object and what's an external file. These are not strict rules - variable names like `variable_name` are also acceptable. The most important thing is to be consistent - choose one style of variable, object and file names, and stick with it!__

```r
# Variable names
 avg.clicks  # Good.
 avg_clicks  # Acceptable.
 avg_Clicks  # Not that okay.

# Function names
 calculate.avg.clicks  # This is what we are aiming for.
 CalculateAvgClicks  # Not that bad, but mixing capital and lowercase letters can lead to typos
 calculate_avg_clicks , calculateAvgClicks  # Bad.
```

#### 2.2 Spacing

__Place spaces around all infix operators (`=`, `+`, `-`, `<-`, etc.).__ The same rule applies when using `=` in function calls.
__Always put a space after a comma, and never before, just like in normal prose.__

There are two exceptions to this rule (that we know of): `:` and `::` don't need spaces around them, and one should not add spaces when defining coordinate systems in spatial objects.

```r
x <- 1:10  # Good
base::get  # Good
dplyr::select  # When you use `package_name::function_name` in your code like the example here, this means you are calling the function `select()` from the package `dplyr` - this way of using functions works without having loaded the package beforehand using `library(dplyr)`, but it's not very commonly used, since it's longer.

crs.geo <- CRS("+proj=longlat +ellps=WGS84 +datum=WGS84")  # geographical, datum WGS84
# Here we are creating an imaginary object with a geographical projection commonly used for the UK
```

__Don't place a space before left parentheses, except in a function call.__

```r
# Good
if (debug) do(x)
plot(x, y)

# Bad
if(debug)do(x)
plot (x, y)
```

__Extra spacing (i.e., more than one space in a row) is ok if it improves alignment of equal signs or assignments (`<-`).__

```r
# Sample code just to illustrate the point, no need to run the code at this point!
LPI_biome_summ <- LPI_long %>%
  group_by(biome) %>%  # Group by biome
  summarise(populations = n(),   # Create columns, number of populations
            mean_study_length_years = mean(lengthyear),  # mean study length
            max_lat = max(decimal_latitude),  # max latitude
            min_lat = min(decimal_latitude),  # max longitude
            dominant_sampling_method = names(which.max(table(sampling_method))),  # modal sampling method
            dominant_units = names(which.max(table(units))))  # modal unit type
```

__Do not place spaces around code in parentheses or square brackets (unless there's a comma, in which case see above).__

```r
# Good
if (debug) do(x)
diamonds[5, ]

# Bad
if ( debug ) do(x)  # No spaces around debug
x[1,]   # Needs a space after the comma
x[1 ,]  # Space goes after comma not before
```

__Inline commenting__ - If you are commenting inline with code, place  __two spaces__ after the code, followed by `#`, a __single space__ and then your text, e.g. `summary(model)<space><space>#<space>comment`.

```r
# Calculating summary statistics for each biome in the Living Planet Index database
# No need to copy and run this code now, this just illustrates comments
LPI_biome_summ <- LPI2 %>%
  group_by(biome) %>%  # Group by biome
  summarise(populations = n(),   # Create columns, number of populations
            mean_study_length_years = mean(lengthyear),  # mean study length
            max_lat = max(decimal_latitude),  # max latitude
            min_lat = min(decimal_latitude),  # max longitude
            dominant_sampling_method = names(which.max(table(sampling_method))),  # modal sampling method
            dominant_units = names(which.max(table(units))))  # modal unit type
```


#### 2.3 Curly braces

An opening curly brace should never go on its own line and should always be followed by a new line. A closing curly brace should always go on its own line, unless it's followed by `else`.
__Always indent the code inside curly braces.__

```r
# Good

if (y < 0 && debug) {
  message("Y is negative")
}

if (y == 0) {
  log(x)
} else {
  y ^ x
}

# Bad

if (y < 0 && debug)
{message("Y is negative")}

if (y == 0) {
  log(x)
}
else {
  y ^ x
}
```

It's ok to leave very short statements on the same line:
```r
if (y < 0 && debug) message("Y is negative")
```


#### 2.4 Line length

__The official convention is to limit your code to 80 characters per line.__ Having to continuously scroll left and right can be annoying and confusing. Also, when you publish your code on Github, the scroll bar is all the way down at the bottom of the page, so to scroll right, you first need to scroll all the way down, scroll right, then scroll all the way up to wherever you want to be ... unnecessary.

__How do you know what's 80 characters though? RStudio can place a handy line in your editor as a reminder! Go to `Tools/Global Options/Code/Display/Show Margin/80 characters`.__ Sometimes it might make more sense for your code to be a bit longer than 80 characters, but in general code is easier to read if there is no need for continuous scrolling left and right, around 100 characters should work alright.

##### When using pipes, keep the pipe operator `%>%` at the end of the line and continue your pipe on a new line.

```r
# Just an example of what a pipe could look like, no need to run the code at this stage.
LPI_long <- LPI_long %>%
  group_by(., genus_species_id) %>%  # group rows so that each group is one population
  mutate(., maxyear = max(year), minyear = min(year)) %>%  # Create columns for the first and most recent years that data was collected
  mutate(., lengthyear = maxyear-minyear) %>%  # Create a column for the length of time data available
  mutate(., scalepop = (pop-min(pop))/(max(pop)-min(pop))) %>%  # Scale population trend data
  filter(., is.finite(scalepop)) %>%
  filter(., lengthyear > 5) %>%  # Only keep rows with more than 5 years of data
  ungroup(.)  # Remove any groupings you've greated in the pipe, not entirely necessary but it's better to be safe
```

##### When using `ggplot2`, keep the `+` at the end of the line and continue adding on layers on a new line.

```r
# Just an example of what the code could look like, no need to run the code at this stage.
vulture_scatter <- ggplot(vultureITCR, aes (x = year, y = abundance, colour = Country.list)) +
    geom_point(size = 2) +                                                
    geom_smooth(method = lm, aes(fill = Country.list)) +                    
    theme_my_own() +
    scale_fill_manual(values = c("#EE7600", "#00868B")) +               
    scale_colour_manual(values = c("#EE7600", "#00868B"),               
                        labels = c("Croatia", "Italy")) +                 
    ylab("Griffon vulture abundance\n") +                             
    xlab("\nYear")
```

#### 2.5 Indentation
If a function definition runs over multiple lines, indent the second line to where the definition starts - you can check out the indentation in the `ggplot2` code above - when you click `Enter` after the `+` sign, the new line automatically gets indented.

Here is a before and after of a `ggplot2` figure code:

```r
ggplot()+geom_hline(yintercept=0,linetype="dotted",colour="darkgrey")+
  geom_line(data=cwa.sub, aes(x=Season,y=Total.Concentration),size=2,alpha=0.2)+
  geom_ribbon(data=preds2, aes(x=Season, ymin=ploBT, ymax=phiBT), fill="#3cd0ea", alpha=0.3)+
  geom_line(data=preds2,aes(x=Season,y=Total.ConcentrationBT),colour="#3cd0ea",size=3)+theme_bw()+ylab("Minimum Sea Ice Concentration")+xlab("Season")+annotate("text",x=2012,y=0.4,label=paste0("p = ",round(pval.cwa.sub,4)),size=6)+theme(legend.title=element_text(size=20,face="plain",hjust=1),legend.text=element_text(size=18,angle=45),legend.position="bottom",legend.key =element_blank(),axis.title.x=element_text(size=20,margin=margin(20,0,0,0)),axis.title.y=element_text(size=20,margin=margin(0,20,0,0)),axis.text=element_text(size=16),panel.grid.minor=element_blank(),panel.grid.major=element_blank())

ggplot() +
  geom_hline(yintercept = 0, linetype = "dotted", colour = "darkgrey") +
  geom_line(data = cwa.sub, aes(x = Season, y = Total.Concentration), size = 2, alpha = 0.2) +
  geom_ribbon(data = preds2, aes(x = Season, ymin = ploBT, ymax = phiBT), fill = "#3cd0ea", alpha = 0.3) +
  geom_line(data = preds2, aes(x = Season, y = Total.ConcentrationBT), colour = "#3cd0ea", size = 3) +
  theme_bw() +
  labs(y = "Minimum Sea Ice Concentration", x = "Season") +
  annotate("text", x = 2012, y = 0.4, label = paste("p = ", round(pval.cwa.sub,4)), size = 6) +
  theme(legend.title = element_text(size = 20, face = "plain", hjust = 1),
        legend.text = element_text(size = 18, angle = 45),
        legend.position = "bottom",
        legend.key = element_blank(),
        axis.title.x = element_text(size = 20, margin = margin(20,0,0,0)),
        axis.title.y = element_text(size = 20, margin = margin(0,20,0,0)),
        axis.text = element_text(size=16),
        panel.grid.minor = element_blank(),
        panel.grid.major = element_blank())
# The second version is much easier to read and there is no need to keep scrolling left and right.
```

<a name="tidy"></a>

### 3. Tidying up old scripts and data frames

It's best to start following a sensible coding etiquette from the very beginning, but realistically we are often in a hurry, we want to code quickly and even if we know we are not following best practices, we still go ahead, because we are thinking of our short-term goals - getting it done, as opposed to the more long-term goals of having a sensible and reproducible record of our analysis. As we are writing this tutorial, we are just as guilty as everyone else of having messy scripts, missing spaces around `=`, etc. But it's important to try to be consistent with your coding, and once you get into the habit of it, it hopefully won't seem "just like one extra thing to do".

#### __What if you want to make your old code neater?__

That's a lot of spaces you might need to add in... First, you could try using RStudio to format the code for you - click on `Code/Reformat code` and see what happens - you will get all the spaces in, but R puts the code on a new line after each comma, too many lines! You can try this instead: (__back up your scripts before you start any experimenting!!!__)

```r
# Reformat your old code to add in spaces and limit line length
install.packages("formatR")
library("formatR")

# Set working directory to wherever your messy script is
tidy_source("messy_script_2017-02-25.R", file = "tidy_script_2017-02-25.R", width.cutoff = 100)
# If you don't specify file = "new_script.R", your script will get overwritten, dangerous!
# If you don't specify a width cutoff point, tidy_source just adds in the spaces
# 100 characters seems like a reasonable cutoff point

# Reformat all the scripts in a directory
# Set your working directory to wherever your messy scripts are

# IMPORTANT this will override script files, so make a duplicate back up folder, in case tidy_dir messes up
tidy_dir(path="whatever/your/path/is", recursive = TRUE)
# recursive	- whether to look for R scripts in subdirectories of the directory specified under path
```

#### Renaming old objects and variables

If, like us, you find yourself having to use a script from before you knew any better, you might have objects with really uninformative, unnecesarily hard to type names. There is an easy fix to that - just like in most text editors, you can `Find` and `Replace` words, in our case object names. You can type up the object whose name you want to change, then add the new one, and replace either individual occurrences, or all of the occasions when the object name is mentioned. You can also select lines of code and only rename the object in that part of the code - careful that you have clicked on `In selection`, as otherwise the object name will be replaced in the entire script, despite you having selected only some of the lines.

<center> <img src="{{ site.baseurl }}/img/replace.png" alt="Img" style="width: 800px;"/> </center>

__If you want to rename your variable names, that's quickly done, too.__

```r
names(dataframe) <- gsub(".", "_", names(dataframe), fixed = TRUE)
# This code takes all of the variable names in the imaginary dataset `dataframe` and replaces `.` with `_`
# Depending on the naming style you are using, you might want to go the other way around and use `.` in all variable names

names(dataframe) <- tolower(names(dataframe))
# This code makes all of the variable names in the imaginary dataset lowercase

colnames(dataframe)[colnames(dataframe) == 'Old_Complicated_Name'] <- 'new.simple.name'
# Renaming an individual column in the imaginary dataset
```

### RStudio addins:

RStudio addins are available for the newest version of RStudio and add some functionality to RStudio using point and click menus. After you have installed certain addins, you can access them by clicking on `Addins`, which is under the `Profile` and `Tools` bar in the RStudio menu. To get a full list of RStudio plugins, run:

```r
install.packages('addinslist')
```

When you click on `Addins/Browse RStudio Addins` you will see the list of addins and the links to their Github repos.

__Boxes around introductory sections of scripts have become a trendy addition to script files, definitely not an essential component, but if that appeals to you, you can add a box using this plugin, saving you the time of typing up many hashtags.__

```r
# Insert a box around the introductory section of your script
install.packages("devtools")
devtools::install_github("ThinkRstat/littleboxes")

# Afterwards select your introductory comments, click on Addins/ Little boxes and the box appears!
# Note that if you are also reformatting your code using formatR, reformat the code first, then add the box.
# formatR messes up these boxes otherwise!
```

<center> <img src="{{ site.baseurl }}/img/boxes.png" alt="Img" style="width: 800px;"/> </center>

Our coding etiquette was developed with the help of <a href="http://adv-r.had.co.nz/Style.html" target="_blank">Hadley Whickham's R Style Guide</a>.

<hr>
<hr>

<h3><a href="https://www.surveymonkey.co.uk/r/8YBXTMT" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
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



