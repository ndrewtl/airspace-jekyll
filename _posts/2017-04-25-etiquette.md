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

When analysing data in `R`, the lines of code can quickly pile up - hundreds of lines to scroll through, numerous objects whose names might make sense to you, but not to other people or future you. This tutorial offers tips on how to make your code easy to read and understand, for yourself and others who may want to read your code in the future. Following a coding etiquette (a set of "rules" you follow consistently throughout your work) will improve your `R` workflow, and reduce the occurrence of annoying errors. 

The coding etiquette outlined in this tutorial is applicable to most analyses and much of it is also applicable to other programming languages.

__We recommend that you follow the tutorial by typing code from the examples into a blank script file to build your own example script file with perfect formatting and etiquette. After you have done that, use your knowledge of coding etiquette to improve the formatting of `bad_script.R`, which you can find in <a href="https://github.com/ourcodingclub/CC-etiquette" target="_blank">the github repository for this tutorial</a>. Alternatively, feel free to edit some of your own scripts using the etiquette guidelines.__ 

### You can download all the resources for the tutorial, including some helpful cheatsheets from <a href="https://github.com/ourcodingclub/CC-Etiquette" target="_blank">this github repository.</a> Clone and download the repo as a zipfile, then unzip it so it appears as a folder.

Alternatively, you can fork [the repository](https://github.com/ourcodingclub/CC-etiquette) to your own Github account and then add it as a new RStudio project by copying the HTTPS/SSH link. For more details on how to register on Github, download Git, sync RStudio and Github and use version control, please check out our previous <a href="https://ourcodingclub.github.io/2017/02/27/git.html" target="_blank">tutorial.</a>

<a name="sections"></a>

### 1. Organising scripts into sections

As with any piece of writing, when writing an R script it really helps to have a clear structure. A script is a `.R` file that contains your code - you could directly type code into the R console, but that way you have no record of it, and you won't be able to reuse it later. To make a new `.R` file, open RStudio and go to `File/New file/R script`. For more information on the general RStudio layout, you can check out our <a href="https://ourcodingclub.github.io/2016/11/13/intro-to-r.html" target="_blank">Intro to RStudio tutorial</a>. A clearly structured script allows both the writer and the reader to easily navigate through the code to find the desired section. 

The best way to split your script into sections is to use comments. You can define a comment by adding `#` to the start of any line and typing text after it, e.g. `# ggplot of population frequency`. Then underneath that comment you would write the code for making your ggplot. RStudio has a neat feature whereby you can make your sections into an outline, similar to that which you can find in `Microsoft Word`. To add a comment to the outline, type four `-` after your comment text, e.g. `# ggplot of population frequency ----`. To view your outline, click the button as shown below, you can then click an outline item and jump straight to it, no more scrolling!:

<center> <img src="{{ site.baseurl }}/img/outline.png" alt="Img" style="width: 800px;"/> </center>

__NOTE: If you don't see the outline icon, you most likely do not have the newest version of RStudio - if you want to get this feature, you can <a href="https://www.rstudio.com/products/rstudio/download/" target="_blank">download</a> the newest version of RStudio.__

#### Script structure:

__There are no strict rules for the number and names of sections, you can adapt section content to your needs, but in general a script includes the following sections:__

__Introduction__ - Author statement (what does this script do?), author(s) names, contact details and date.

__Libraries__ - What packages are you using for this script? Keep all of them together at the start of your script. When switching between scripts, with your packages already loaded, it's easy to forget to copy across the library, which means future you might get confused as to why the code isn't working anymore. Your library will be extra informative to you and other people if you add in comments about what you are using each package for. Here are two examples, good and bad, to illustrate these first two sections:

A not particularly useful script intro:

```r
# My analysis
```

A more informative script intro:

```r
# Analysing vertebrate population change based on the Living Planet Index
# Data available from http://www.livingplanetindex.org/

# Gergana Daskalova ourcodingclub@gmail.com
# 25-04-2017

# Libraries ----
library(tidyr)  # Formatting data for analysis
library(dplyr)  # Manipulating data
library(ggplot2)  # Visualising results
library(readr)  # Manipulating data
```

__You might have noticed that when you create a section using four or more `-` at the end of a comment line, a little arrow appears in the margin next to the comment. Clicking these arrows allows you to collapse the section, very useful when traversing a long script.__

<center> <img src="{{ site.baseurl }}/img/etiquette_outline.png" alt="Img" style="width: 800px;"/> </center>

__You can also go to `Edit/Folding/Collapse all` to collapse all sections - this is the outline of your script, and from here you can navigate to whichever section you need. `Expand all` displays all of the code you've written. Here is an example:__

<center> <img src="{{ site.baseurl }}/img/outline2.png" alt="Img" style="width: 800px;"/> </center>


__Functions__ - Are you using any functions written by you and/or others? Define them here. For example functions to remove `NA` values, functions to <a href="https://ourcodingclub.github.io/2017/02/08/funandloops.html" target="_blank">create your own `ggplot2` theme.</a> Here is an example functions section:

```r
# Defining functions ----
# A custom ggplot2 function
theme.LPI <- function(){
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

If you run the code for the `ggplot2` theme function above, you will see the name of the function you created appear in your `Global Environment` in the top right corner of your `RStudio` screen (you might need to scroll down past any objects you've created). Once you create a certain function, `RStudio` will remember it for the remainder of your session - if you close `RStudio` and then open it again later, you will need to run the code for the function again. __NOTE: When you close `RStudio`, a message will ask if you want to save your workspace image. If you click yes, the next time you open `RStudio`, it will look exactly as it did when you closed it, with the same objects stored in your `Global environment`. If you click no, the next time you open `RStudio`, you will need to open your script and run through the code again, if you want to use the same objects. We personally don't often save our workspace image - it makes `RStudio` run more slowly, and can introduce errors as you might confuse objects from different analyses and/or overwrite objects without noticing.__

__Setting the working directory__ - It helps to keep all your data, scripts, image outputs etc. in a single folder. This minimises the chance of losing any part of your analysis and makes it easier to move the analysis on your computer without breaking filepaths. Note that filepaths are defined differently on Mac/Linux and Windows machines. On a Mac/Linux machine, user files are found in the 'home' directory (`~`), whereas on a Windows machine files can be placed in multiple 'drives' (e.g. `D:`). Also note that on a Windows machine, if you copy and paste a filepath from Windows Explorer into RStudio, it will appear with backslashes (`\ `), but R requires all filepaths to be written using forward-slashes (`/`), so you will have to change those manually. __Set your working directory to the folder you downloaded from Github earlier, it should be called `CC-etiquette-master`. See below for some examples for both Windows and Mac/Linux:__

```r
# Set the working directory on Windows ----
setwd("D:/Work/coding_club/CC-etiquette-master")

# Set the working directory on Mac/Linux ----
setwd("~/Work/coding_club/CC-etiquette-master")
```

__Importing data__ - what data are you using and where is it stored? __Import `LPIdata_CC.csv` from your working directory__. Here is an example:

```r
# Import data ----
LPI <- read.csv("LPIdata_CC.csv")
```

__The different sections of your analysis__ - what is the logical workflow of your analysis? Keep the order in which you tackle your analysis consistent. If this is code for an undergraduate dissertation, a thesis chapter, or a manuscript, you can follow the same order in your script. Here is an example - if you copy these across to a script file, you'll see the sections appear. Once you have imported in `LPIdata_CC.csv`, run the following code to generate the plot called `barplot`, which you can see in the image below:

```r
# Formatting data ----
LPI2 <- gather(LPI, "year", "abundance", 9:53)  # Transforming the data from wide to long format, some blank cells may disappear
	# gather function requires tidyr package
LPI2$year <- parse_number(LPI2$year)  # Do you see awkward Xs before all the years? This gets rid of them.
names(LPI2)  # Check what the different variables are called
names(LPI2) <- tolower(names(LPI2))  # Make all variable names lower case

# When manipulating data it's always good check if the variables have stayed how we want them
# Use the str() function
str(LPI2)

# Abundance is a character variable, when it should be numeric, let's fix that
LPI2$abundance <- as.numeric(LPI2$abundance)

# Calc summary stats for each biome in the LPI database ----
levels(LPI2$biome)  # list all biomes

LPI_biome_summ <- LPI2 %>%  # use of pipe operator
  group_by(biome) %>%  # Group by biome
  summarise(populations = n())  # Create columns, number of populations

# Visualising the number of populations in each biome ---- 
barplot <- ggplot(LPI_biome_summ, aes(biome, color = biome, y = populations)) + geom_bar(stat = "identity") +  # use of ggplot2 package
  		theme.LPI() +  # use of personal theme function
  		ylab("Number of populations") +
  		xlab("Biome") +
		theme(legend.position = "none")  # removal of legend for simplicity
```

<center><img src="https://ourcodingclub.github.io/img/Biome_pop.png" alt="Img" style="width: 950px;"/></center>
Figure 1. Abundance of species populations for each biome.

__The outputs of your analysis__ - Remember to keep your filepath sensible not only when loading data in, but also when you are outputting files (e.g. `.Rdata`, `.csv` files and any figures you want saved). `.csv` files are more transferable and can be used across multiple platforms, whereas `.Rdata` files are more compressed and are quicker to work with. Saving graphs as `.pdf` files is better practice, since `.pdf` files are vector based and don't decrease in quality when you zoom in or out. `.png` files, on the other hand, are easily inserted in text documents and presentations, so ideally you should save a `.pdf` and a `.png` file of your graph. It is also good practice to save image outputs in a subdirectory of your working directory, e.g. `img/`. Remember that you will have to create the folder `img` manually before saving plots to it:

```r
png(file="img/biome_pop.png", width = 1000, height = 2000)  # Note that png() uses pixel values for width and height
ggplot(LPI_biome_summ, aes(biome, color = biome, y = populations)) + geom_bar(stat = "identity") +
  		theme.LPI() +
  		ylab("Number of populations") +
  		xlab("Biome") +
		theme(legend.position = "none")
dev.off()  # This tells R you are done with the plotting and it can save the file

pdf(file="img/biome_pop.pdf",  width = 13.33, height = 26.66)  # pdf() uses inches
ggplot(LPI_biome_summ, aes(biome, color = biome, y = populations)) + geom_bar(stat = "identity") +
  		theme.LPI() +
  		ylab("Number of populations") +
  		xlab("Biome") +
		theme(legend.position = "none")
dev.off()
```


<a name="syntax"></a>


### 2. Following a coding syntax etiquette

#### 2.1. Naming files and objects.

##### "There are only two hard things in Computer Science: cache invalidation and naming things." - Phil Karlton

We're not too familiar with cache invalidation, but we would definitely agree that naming things is hard, and going for a quick and easy solution, like calling your graphs `graph`, might cause trouble later!

__File names for scripts should be meaningful and end in `.R`. Avoid spaces and funky characters!!! They can cause trouble when uploading files to Github and in general when trying to locate files through certain file paths.__

```r
LPI_analysis_Apr_2017.R  # Alright.

yet_another_script.R  # Bad. Took me hours to find the file when I needed it one year later.
```

__Object names should be concise and meaningful.__

Calling your objects `data` or something similarly vague might cause problems if you are doing multiple analyses at once / don't clean your environment periodically, as these object names will get overwritten, and can mess up your script if you aren't running it in order. 

Long object names are annoying to type. More letters = higher chance you'll make a typo.

Object, variable (e.g.`object$variable`) and function names should be lowercase. `MinPrecip_august` is confusing to remember, `min.precip.aug` is a bit long, but informative and easier to type.

##### - __Variable names should be nouns.__ e.g. `abundance` `richness`
##### - __Function names should be verbs.__ e.g. `calc.sp.richness`
##### - __Use an underscore to separate words within a script file.__ e.g. `LPI_analysis_Apr_2017.R`
##### - __The preferred form for object/variable names is all lower case letters and words separated with underscores__ e.g. (`object_name$variable_name`).
##### - __For functions all lower case letters and words separated by dots__ e.g. (`function.name`).

__This way it is clear what is an object and what is an external file. These are not strict rules - variable names like `variable_name` are also acceptable. The most important thing is to be consistent - choose one style of variable, object and file names, and stick with it!__

```r
# Object names
 avg_clicks  # Good.
 avg.clicks  # Acceptable.
 avg_Clicks  # Not okay.

# Function names
 calculate.avg.clicks  # This is what we are aiming for.
 CalculateAvgClicks  # Not that bad, but mixing capital and lowercase letters can lead to typos
 calculate_avg_clicks , calculateAvgClicks  # Bad. The convention is that functions are defined using dots, not underscores.
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

__The official convention is to limit your code to 80 characters per line.__ Having to continuously scroll left and right can be annoying and confusing. Also, when you publish your code to Github, the scroll bar is all the way down at the bottom of the page, so to scroll right, you first need to scroll all the way down, scroll right, then scroll all the way up to wherever you want to be ... unnecessary.

__How do you know what's 80 characters though? RStudio can place a handy line in your editor as a reminder! Go to `Tools/Global Options/Code/Display/Show Margin/80 characters`.__ Sometimes it might make more sense for your code to be a bit longer than 80 characters, but in general code is easier to read if there is no need for continuous scrolling left and right, around 100 characters should work alright.

##### When using pipes from the `dplyr` package, keep the pipe operator `%>%` at the end of the line and continue your pipe on a new line.

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
If a command runs over multiple lines, indent the second line to where the definition starts - you can check out the indentation in the `ggplot2` code above - when you click `Enter` after the `+` sign, the new line automatically gets indented.

Here is a before and after of a `ggplot2` figure code:

```r
# Again, just an example, don't run this, it won't work!
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

__Now that you have read through the tutorial, try to clean up `bad_script.R`, which can be found in <a href="https://github.com/ourcodingclub/CC-etiquette" target="_blank">the github repository for this tutorial</a>, or tidy up one of your own scripts.__ 

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



