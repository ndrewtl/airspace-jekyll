---
layout: post
title: Transferring quantitative skills among scientists
subtitle: How to publish and share statistics and programming tutorials
date: 2017-11-23 10:00:00
author: The Coding Club Team
meta: "Tutorials"
tags: github
---

<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheadertut.png" alt="Img">
	</center>
</div>

## Tutorial Aims:

#### <a href="#demo"> 1. Get familiar with the Coding Club model</a>

#### <a href="#tutorial"> 2. Write your own tutorial</a>

#### <a href="#publish"> 3. Publish your tutorial on Github</a>

## Key steps

__Each step is explained in detail as you start going through the tutorial below. Have a quick read, there is no need to click on links or download things right now, this is just an outline, so that you know what is ahead of you. You can use this list as a reference to track how far along the tutorial you are.__

__Step 1. Individually or in small groups, complete <a href="https://ourcodingclub.github.io/2017/11/11/popchange.html" target="_blank">a brief Coding Club tutorial</a> about quantifying and mapping vertebrate population change in Europe.__

__Step 2. In small groups, create your own tutorial.__

__Step 3. Choose a topic for your tutorial from the list we’ve collated, each demonstrator will help out the group that has chosen the topic they contributed.__

__Step 4. Download the tutorial template file `tut_template.md` and the `R` scripts for the various tutorials from <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas">this GitHub repository.</a>__ (click on Clone/Download, Download Zip and unzip the files).

__Step 5. Open the `R` script for your chosen topic, run through the code to get familiar with what it does, save any plots it generates.__

__Step 6. Open `tut_template.md` in a plain text editor on half of your screen. Keep `RStudio` and the `R` script on the other half of the screen.__

__Step 7. Follow the template and instructions to create your tutorial. You need to copy the code from the `R` script to the template fle, add text to explain what your tutorial does and add the plots.__

__Step 8. Save your completed template file as `index.md`.__

__Step 9. Create a new repository on GitHub and upload `index.md` and your plots. Go to Settings, enable GitHub pages - you are done, your tutorial is now live at the link thats shows up in the GitHub pages settings panel!__

<a name="demo"></a>
<center><img src="{{ site.baseurl }}/img/CodingClub_logo2.png" alt="Img" style="width: 700px;"/></center>


__We started Coding Club to help people at all career stages gain statistical and programming fluency, facilitating the collective advancement of ecology across institutions and borders. We use in-person workshops and online tutorials to equip participants not only with new skills, but also with the means to communicate these new skills broadly via online tutorials.__

__We would love to extend Coding Club beyond the University of Edinburgh and create a supportive community of people keen to get better at coding and statistics! With that in mind, we present you with a tutorial on how to write and share tutorials!__


<center><img src="{{ site.baseurl }}/img/74b26610-2027-11e7-841b-f91777fdfcdf.png" alt="Img" style="width: 700px;"/></center>

There are similar initiatives already in place, which is very exciting! For this workshop, we are thrilled to be collaborating with the <a href="https://aberdeenstudygroup.github.io/studyGroup/" target="_blank">Aberdeen Study Group</a>, led by <a href="https://francescamancini.github.io/" target="_blank">Francesca Mancini</a>. The Aberdeen Study Group aims to foster a place where people can get together to work on their coding projects, help each other out and share their work, whilst also learning new skills. You can follow their adventures in coding and open science on <a href="https://twitter.com/abdnStudyGroup" target="_blank">Twitter</a>.

## How does a Coding Club workshop work?
There are many ways to run a coding workshop, and different approaches might work better in different situations. Here is how we usually structure our workshops. The workshops take two hours and begin with a super short presentation or introductory talk about what we will be doing, what skills we will acquire and what they are useful for. We then direct workshop attendants to the link for the tutorial around which the workshop is focused. People usually open the tutorial on half of their screen, and `RStudio` on the other half of their screen.

<center><img src="{{ site.baseurl }}/img/workshop.png" alt="Img" style="width: 650px;"/></center>

At each workshop, we have a team of demonstrators who are there to answer questions and help out. We find that it works well to let people go through the tutorial at their own pace, and we usually walk around and check whether things are going fine. Most of the tutorials have challenges at the end, for which people can work individually or in small teams. We bring cookies, popcorn and other treats, occasionally make bad R jokes, and try our best to make the atmosphere light and positive. We don't require people to sign up and there are no obligations to attend all the workshops - people are free to attend whichever workshops are of interest to them. At the end of the workshops, we usually stay behind for a while in case people have any specific questions about their own coding projects.

## Find out for yourself - complete a quick Coding Club tutorial


#### To get a taste of the Coding Club experience, you can complete a <a href="https://ourcodingclub.github.io/2017/11/11/popchange.html" target="_blank">Coding Club tutorial on mapping vertebrate population change across Europe.</a>

<center><img src="{{ site.baseurl }}/img/anseriformes.png" alt="Img" style="width: 700px;"/></center>
<center><p><i>Anseriformes</i> populations in Europe.</p></center>


<a name="tutorial"></a>

## Write your own tutorial

__Next we will learn how to write, format and publish coding tutorials.__

We write our tutorials in Markdown. Markdown is a language with plain text formatting syntax. Github and Markdown work very well together, and we use Markdown, because we can turn a Markdown file into a website hosted on Github in a minute or so! Because of the syntax formatting, Markdown is a great way to display code - the code appears in chunks and stands out from the rest of the text. All of the Coding Club tutorials are written in Markdown.

We use the Atom text editor, which is user-friendly text editor and easy on the eyes. You can use another text editor, like Brackets or Text Edit a Mac and Notepad on a Windows computer, if you prefer, the principle is the same - you just a plain text editor. A plain text editor is a programme, which allow you to create, save and edit various types of text files, like `.txt` and in our case, `.md` files. So for example, `Microsoft Word` is a text editor, but not a plain one, and you can't easily save `.md` files. In the "fancier" plain text editors, you get "syntax" highlighting - different types of text, like code and links, are colour coded, so they are easier to spot.

__You can <a href="https://atom.io/" target="_blank">download Atom here, if you wish.</a>__

<center><img src="{{ site.baseurl }}/img/atom_rstudio.png" alt="Img" style="width: 1000px;"/></center>


Our workflow tends to go like this:

#### - Write the `R` code for the tutorial in `RStudio`

#### - Save any graphs you create with your code

#### - Open `Atom`, copy and paste your `R` code in a new file

#### - Save the file as a `.md` file, e.g. `datavis.md`

#### - Add text to explain the purpose of the tutorial and what the code does

#### - Add images and links as suitable


#### Don't worry if you've never used `Atom` or `Markdown` before - we have created a template you can open straight in Atom (or another plain text editor) and just insert your text, comments and images.


### You can download the  `tut_template.md` file that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them.


__Open the file `tut_template.md` in Atom. The file includes instructions on how to add subheadings, links, code and images. We have prepared a few sample topics based on which you can write a brief tutorial. Please choose a topic by clicking on it, which will take you to all the files necessary to write the tutorial.__

<section id="portfolio-work">
    <div class="container">
        <div class="row">
          <div class="col-md-12">
            <div class="block">
              <div class="portfolio-contant">
                <ul id="portfolio-contant-active">
                    <li>
                      <a href="#polar_map">
                        <img src="{{ site.baseurl }}/img/portfolio/arctic_fox_icon.png" alt="">
                        <div class="overly">
                          <div class="position-center">
                            <center><h2>Mapping species occurrence records</h2></center>
                            <center><p>A circumporal map of Arctic Fox occurrences</p></center>
                          </div>
                        </div>
                      </a>
                  </li>
                    <li>
                      <a href="#forest_plots">
                        <img src="{{ site.baseurl }}/img/portfolio/elephants_icon.png" alt="">
                        <div class="overly">
                          <div class="position-center">
                            <center><h2>Plotting forest plot tree data</h2></center>
                            <center><p>The effects of elephant activity</p></center>
                          </div>
                        </div>
                      </a>
                  </li>
		<li>
		  <a href="#density_maps">
		   <img src="{{ site.baseurl }}/img/portfolio/density_rs_icon.png" alt="">
		   <div class="overly">
		   <div class="position-center">
		   <center><h2>Visualising species occurrence data</h2></center>
		   <center><p>Density maps of red squirrel occurrences</p></center>
		        </div>
		     </div>
		  </a>
		</li>
		<li>
		  <a href="#temp_timeseries">
		<img src="{{ site.baseurl }}/img/portfolio/timesr_icon.png" alt="">
		     <div class="overly">
		      <div class="position-center">
		    <center><h2>Visualising temperature time series data</h2></center>
		   <center><p>Plotting mean daily temperatures and fluctuations</p></center>
		    </div>
	          </div>
		</a>
		</li>
		<li>
		  <a href="#plant_traits">
		   <img src="{{ site.baseurl }}/img/portfolio/traits_icon.png" alt="">
		   <div class="overly">
		   <div class="position-center">
		   <center><h2>Summarising plant tree data</h2></center>
		   <center><p>Manipulating and visualising plant traits</p></center>
		        </div>
		     </div>
		  </a>
		</li>

                </ul>
              </div>
            </div>
          </div>
        </div>
    </div>
</section>

<a name="polar_map"></a>

## Mapping species occurrence records
#### By Gergana Daskalova

__The aims of this tutorial are to download species occurrence data from GBIF using the `rgbif` package, and then plot the data. We will also learn how to create a map with a top-down view of the world, as the species we've chosen, Arctic fox, is found in the Northern hemisphere.__

<center> <img src="{{ site.baseurl }}/img/fox_map.png" alt="Img" style="width: 500px;"/>   <img src="{{ site.baseurl }}/img/fox_map2.png" alt="Img" style="width: 500px;"/></center>
<center>Arctic fox occurrences based on available data from the Global Biodiversity Information Facility (GBIF).</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script is the `arctic_map.R` file in the `arctic_fox` folder.


<a name="forest_plots"></a>

## Visualising forest plot tree data
#### By John Godlee

__This tutorial involves plotting tree inventory data from two permanent survey plots in a dry tropical savannah to see how spatial clustering of trees varies according to elephant activity. The tutorial covers the basics of using the `ggplot2` package, using multiple layered visualisation methods to show variation in tree abundance over space. In addition, the tutorial will touch on  simple skills in the immensely popular `dplyr` package to prepare datasets for use in data visualisation.__

<center> <img src="{{ site.baseurl }}/img/elephant_plot.png" alt="Img" style="width: 500px;"/>   <img src="{{ site.baseurl }}/img/no_elephant_plot.png" alt="Img" style="width: 500px;"/></center>
<center>The spatial clustering of trees in a plot with elephant activity (left) and without elephant activity (right). Elephants clearly have caused spatial clustering of trees.</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The data and script for this tutorial are in the `savanna_elephants` folder.


<a name="density_maps"></a>

## Density maps of red squirrel occurrences
#### By Francesca Mancini

__The tutorial will take you through the steps of downloading red squirrel occurrences in the UK from the Global Biodiversity Information Facility (GBIF), adjusting spatial projections and plot density maps with `ggplot2`.__

<center> <img src="{{ site.baseurl }}/img/density_rs.png" alt="Img" style="width: 600px;"/> </center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script for this tutorial `density_maps.R` is in the `density_maps` folder.


<a name="temp_timeseries"></a>

## Visualising temperature timeseries data
#### By Anders Kolstrad

__The aim of this tutorial is to produce a line graph or time series plot with mean daily temperature plus errors using `ggplot2`, and similarly, to produce a second graph of daily temperature fluctuations using a smoother function. Finally, we will plot and save the two figures together using the `gridExtra` package.__

<center> <img src="{{ site.baseurl }}/img/temp_fluctuations.png" alt="Img" style="width: 600px;"/> </center>
<center>Daily temperature fluctuations in 2016.</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script for this tutorial `temp_time_series.R` is in the `temp_timeseries` folder.

<a name="plant_traits"></a>

## Visualising trait-trait correlations and summarising plant traits across species
#### By Anne Bjorkman

<center> <img src="{{ site.baseurl }}/img/traits.png" alt="Img" style="width: 800px;"/> </center>
<center>Plant traits across different species.</center>

__The aims of this tutorial are to create a trait-trait correlation plot using plant trait data in a wide format, then to convert this wide data format to long data format, to summarize the data (i.e., calculate a mean, max, min, range, and quantiles per trait and species), and finally to graph the raw and summarized data.__

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script for this tutorial `Plant_Traits.R` and the data `TraitData_CodingClub.RData` are in the `plant_traits` folder.


<a name="spatial_movement"></a>

## Analysis of spatial movement
#### By Stefano Masier

__The aim of this tutorial is to visualize data from a series of geographical coordinates, plot them and extract some basic information. The goal is to handle a series of coordinates, plot the path itself, but also to calculate and plot the covered distance, the relative movement and the relative angle for each time step. This information can then be used as a starting point to more advanced statistical analysis (i.e. GLMs).__

*Coming soon*


<a name="sunflecks"></a>

## Analysing leaf-level understorey photosynthesis within sunflecks
#### Dries Landuyt

__In this tutorial, we will learn to work with pipes `%>%` and other `dplyr` functions, as well as different plotting techniques using the `ggplot2` package. We will apply our data maninpulation and data visualisation skilss to explore the importance of sunflecks for carbon assimilation in an understorey herb based on a LICOR dataset (leaf-level gas exchange measurements) with a temporal resolution of 5 seconds, gathered on a sunny day in June 2017.__

*Coming soon*


<a name="publish"></a>

# Publish your tutorial on Github

__Next we can publish out tutorial on GitHub, which will turn it into a website, whose link you can share with your peers - transferring quantitative skills among ecologists in action!__

__Go to the GitHub website, register if you don't already have an account(it's free) and click on `New Repository`.__

<center> <img src="{{ site.baseurl }}/img/new_repo_eab.png" alt="Img" style="width: 600px;"/> </center>

Choose a name for your repository - that will form part of the link for your online tutorial, so choose something short and informative. Add a brief description, click on `Initialize with a README.md`, and then click on `Create repository`.

<center> <img src="{{ site.baseurl }}/img/new_repo_eab2.png" alt="Img" style="width: 600px;"/> </center>

#### Now you can see your new repository. Click on `Upload files` and upload your filled in `Markdown` template. Make sure you save the file as `index.md` - that will make your tutorial the landing (home) page of the website. Upload any images you are using in your tutorial as well.

You are two clicks away from having a website with your tutorial! Now click on `Settings` and scroll down to the `GitHub pages` section - we need to enable the `GitHub pages` feature, which turns our `index.md` file into a page, i.e. website. Change `Source` from `None` to `master` - the master branch of our repository. Click on `Save`.

<center> <img src="{{ site.baseurl }}/img/github_pages.png" alt="Img" style="width: 600px;"/> </center>

#### Congratulations, your repository is now published as a website!

__Scroll down to the `GitHub pages` section again - you can see the link for your tutorial! If you need to edit your tutorial, you can go back to your repository, select the `index.md` file, then click on `Edit` and make any necessary changes. You can also check out different themes for your website, though the default one is clean and tidy, which works well for coding and statistics tutorials in general.__

### We would love to see your tutorials - feel free to share them with us on Twitter __@our_codingclub__ or via email __ourcodingclub@gmail.com__

### Contribute a tutorial

__Are you keen to share some of your coding and statistics knowledge? We would love to have more people join our team and build a world-wide community of people teaching and learning together! You can take a look at the tutorials we have already developed - feel free to make suggestions for changes on existing tutorials and get in touch with us at ourcodingclub@gmail.com if you would like to make a new tutorial.__

### Useful resources

You can also make a website with multiple pages, rather that having a single page (your `index.md` file). That's how we've made the <a href="https://ourcodingclub.github.io/" target="_blank">Coding Club website and the <a href="https://aberdeenstudygroup.github.io/studyGroup/" target="_blank">Aberdeen Study Group website</a>.
	
__The Mozilla Science Lab has <a href="https://github.com/mozillascience/studyGroup" target="_blank">a template</a> you can use for your website and <a href="https://mozillascience.github.io/study-group-orientation/index.html" target="_blank">a guide on how to use it</a>.__


<hr>
<hr>

<h3><a href="SURVEY_MONKEY_LINK" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
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
