---
layout: post
title: Troubleshooting and how to find help
subtitle: How to avoid common mistakes in R
date: 2016-11-15 17:11:27
author: Gergana
meta: "RBasics"
---
<div class="block">
          <center><img src="{{ site.baseurl }}/img/tutheader2.png" alt="Img"></center>
        </div>

### Tutorial aims:

#### 1. Learn how to pick up on errors in R

#### 2. Learn how to interpret error messages

#### 3. Find help and solutions online

### Steps:

#### <a href="#id">1. Identify how R reports errors</a>

#### <a href="#errors">2. Get familiar with a range of R error messages</a>

#### <a href="#help">3. Identify useful websites and online resources</a>

In our first tutorial we learned how to import data into RStudio, conduct a simple analysis (calculate species richness) and plot the results. Here, we will build up on that knowledge by getting up to grips with common coding errors and how to avoid them - you might have seen some of these error messages already, but after completing this tutorial, we hope they won't make an appearance all to often of your RStudio screens.

<a name="id"></a>

### 1. Identify how R reports errors

In addition to keeping a record of your code, scripts are also useful for detecting simple coding errors before you've even run the code. If R picks up on a character missing, a command that doesn't make sense due to spelling errors or similar, a little <i>x</i> appears next to that line of code - scanning your code for <i>x</i>'s before running it is always a good idea and it's very convenient since you know exactly on which line you made a mistake. The other way R reports errors is through messages in the console - those appear after you have ran code that is not quite right. Although the error messages look scary (the red font and words like "fatal" sure give them a bad reputation), they are actually the second best option to no errors at all - R has identified there is a problem and from the message, you can figure out what it is and solve it!

<div class="block">
          <center><img src="{{ site.baseurl }}/img/xandm.png" alt="Img"></center>
        </div>

<a name="errors"></a>

### 2. Get familiar with common errors

Here we have compiled a list of mistakes we often make. Do you think we have forgotten an error message or problem you encounter often? Please let us know at ourcodingclub@gmail.com and we will add it to our list!

1. <b>Your version of RStudio is too old or too new.</b> If you haven't updated RStudio in a while, you might not be able to use some of the new packages coming out - when you try installing the package, you will get an error message saying that the package is not compatible with your version of RStudio - the problem is quickly fixed by a visit to the <a href="https://www.rstudio.com/products/rstudio/">RStudio website</a> from there you can get the most recent version. On the flip side, when you get the newest RStudio, packages that haven't been updated recently might not work, or old code you wrote breaks - this occurs less often and in general, code is ever evolving and getting better and better, so it's good to keep up to date with the latest versions of both RStudio and R packages.

2. <b>You're trying to use a certain function and R doesn't recognise it.</b> First, it's worth checking whether you have installed and loaded the package the function comes from - if you are reading up on R online, or copying and modifying code, you might be using a function from a new package without knowing - if it looks unfamiliar, googling its name with "r package" might reveal its origin. Sometimes packages depend on other packages to run - often those get installed automatically when you install the package, but sometimes you get an error message asking you to install another package, easily solved by `install.packages("newpackage")`.

3. <b>Syntax errors.</b> The easiest mistakes to make - you've forgotten a comma, opened a bracket, but haven't closed it, added an extra character by mistake. Those are usually picked up by R and you will get error messages reminding you to prood-read your code and fix them. If you can't pinpoint what's the correct way to code what you need, there are many <a href="#help">places to find help.</a>

4. <b>Missing objects.</b> Running tests and plotting data are often hindered by R failing to find the object it's meant to analyse. When that happens, check that how you have called your object and whether how you refer to it is consistent - spelling mistakes (capital and lower case letters, wrong letters, etc.) can all make objects unrecognisable. In this code `e <- length(unique(FloweringPlants$taxonName))` I asked R to calculate species richness of flowering plants, but forgot that I called the object `Flowering.Plants`, not `FloweringPlants`. Remember that when you refer to a certain variable from an object with the dollar sign, the object comes first, the variable second - `Flowering.Plants$taxonGroup`, not `taxonGroup$Flowering.Plants`.

5. <b>Data not in the right format.</b> In our first tutorial we created a data frame and plotted species richness - if we had chosen a data matrix instead, though, that plot would have looked way different (and wrong). We use matrices when the variables are all the same type (all text, all numerical) and of the same length (so same number of rows). Data frames for when we have multiple variables of different types, and vectors for a series of numbers. If your results/plots make you feel suspicious, it's good to go back to your data and check - did it import right into R (here is how to check), and is it in the right format?

<div class="block">
          <center><img src="{{ site.baseurl }}/img/wrong.png" alt="Img"></center>
        </div>
Figure 1. An unfortunate looking barplot - because in matrices all variables are of the same type, here R expects taxa_f - the names of the different taxa - to have a numerical value, and lumps all the species richness values together in the second bar.

6. <b>Wrong data distribution used in models.</b> There are several reasons why models won't converge, including the use in inappropriate distribution type - usually we choose between normal (gaussian), binomial, Poisson, or Quasipoisson distributions - we will learn more about when to use each of them in our workshops on modelling.

6. <b>R crashed!</b> If you've overloaded R, it can make a dramatic exit (bomb image and all), or sometimes it stops responding and you have to terminate the session. That is why it's very important to save your scripts often, but it's better to save them as new files, e.g. Edi_biodiv_16thNov.R, instead of overwriting the same file - that way if you want to revert back to old code or use some part of it, it's easy to find it. This is the most basic type of version control - we will learn more about version control in future tutorials.

<div class="block">
          <center><img src="{{ site.baseurl }}/img/bomb.png" alt="Img"></center>
        </div>

7. <b>I am stuck in a loop of pluses!</b> If the number of opening and closing brackets don't match up, R thinks there is more code coming, that is why in the console it is prompting you to add more code - every time you press enter, a new + appears. Press <i>Escape</i> on your keyboard to get back to the normal `>` prompt in the console and check your code to find your error.

<div class="block">
          <center><img src="{{ site.baseurl }}/img/pluses.png" alt="Img"></center>
        </div>

8. <b>The cursor in the script file changed from | to _ and now text gets overwritten when I type.<b> This happens when you accidentally press <i>Insert</i> on your keyboard and as a result when you add new text, the old text after it get written over. Press <i>Insert</i> again to go back to normal.

<a name="help"></a>

### 3. Find help online

Copying and googling the error message is always a good start - chances are someone has already encountered that problem and has asked about it online. If the error message is very long, try paraphrasing based on what you think the problem might be. There are several really useful online forums and websites where people ask for and receive help, such as <a href="http://stackoverflow.com ">Stackoverflow</a> and <a href="https://www.r-bloggers.com/">Rbloggers</a>.

For "how to ..." type queries, a google search will often result in tutorials, and there might be Youtube videos as well.

Finally, we are currently compiling a "Useful links" list of helpful websites and tutorials - we will be adding it soon, so keen an eye out!

Of course, R won't always tell you if you are doing something wrong - sometimes your code is correct, but you are doing the wrong type of analysis for your data. Nevertheless, making sure you avoid the common but oh so easy mistakes is a great point to start on - even the most complex of tests can be brought down by a missing comma.

### Tutorial outcomes:

#### 1. You know how R reports errors - both in script files and in the console

#### 2. You can solve common mistakes in R

#### 3. If you can't figure out a solution yourself, you know where to find help
