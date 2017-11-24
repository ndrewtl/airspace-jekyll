---
layout: post
title: Transferring quantitative skills among scientists
subtitle: How to publish and share statistics and programming tutorials
date: 2017-11-23 10:00:00
author: Coding Club Team
meta: "Tutorials"
tags: datavis modelling data_manip github
---

<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheadertut.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#demo"> 1. Get familiar with the Coding Club model</a>

#### <a href="#tutorial"> 2. Write your own tutorial</a>

#### <a href="#publish"> 3. Publish your tutorial on Github</a>

<a name="demo"></a>

__We started Coding Club to help people at all career stages gain statistical and programming fluency, facilitating the collective advancement of ecology across institutions and borders. We use in-person workshops and online tutorials to equip participants not only with new skills, but also with the means to communicate these new skills broadly via online tutorials.__

__We would love to extend Coding Club beyond the University of Edinburgh and create a supportive community of people keen to get better at coding and statistics! With that in mind, we present you with a tutorial on how to write and share tutorials!__

## How does a Coding Club workshop work?
There are many ways to run a coding workshop, and different approaches might work better in different situations. Here is how we usually structure our workshops. The workshops take two hours and begin with a super short presentation or introductory talk about what we will be doing, what skills we will acquire and what they are useful for. We then direct workshop attendants to the link for the tutorial around which the workshop is focused. People usually open the tutorial on half of their screen, and `RStudio` on the other half of their screen.

<center><img src="{{ site.baseurl }}/img/workshop.png" alt="Img" style="width: 650px;"/></center>

At each workshop, we have a team of demonstrators who are there to answer questions and help out. We find that it works well to let people go through the tutorial at their own pace, and we usually walk around and check whether things are going fine. Most of the tutorials have challenges at the end, for which people can work individually or in small teams. We bring cookies, popcorn and other treats, occasionally make bad R jokes, and try our best to make the atmosphere light and positive. We don't require people to sign up and there are no obligations to attend all the workshops - people are free to attend whichever workshops are of interest to them. At the end of the workshops, we usually stay behind for a while in case people have any specific questions about their own coding projects.

We welcome people with all levels of R knowledge to our workshops - it's impressive how quickly people can go from never having used R before to making graphs with a bit of help! For the more advanced workshops, we usually send a link with a previous tutorial that provides the base we will build on, but we don't make completing the pre-requisites compulsory - basically we believe that people are free to make their own decisions, and we are there to support them along the way. Sometimes people don't have time to "prepare" and that's okay - it's way better if they show up and we give them a quick intro to bring them up to speed, as opposed to them not showing up at all, because they feel intimidated by the material.

### Find out for yourself - complete a quick Coding Club tutorial


#### To get a taste of the Coding Club experience, you can complete a <a href="https://ourcodingclub.github.io/2017/11/11/popchange.html" target="_blank">Coding Club tutorial on mapping vertebrate population change across Europe.</a>


<a name="tutorial"></a>

### Write your own tutorial

__Next we will learn how to write, format and publish coding tutorials.__

We write our tutorials in Markdown and we use the Atom text editor, which is user-friendly text editor and easy on the eyes. You can use another text editor, like Brackets, if you prefer, the principle is the same.

#### You can <a href="https://atom.io/" target="_blank">download Atom here.</a>

Our workflow tends to go like this:

- Write the `R` code for the tutorial in `RStudio`
- Save any graphs you create with your code
- Open Atom, copy and paste your `R` code in a new file
- Save the file as a `.md` file, e.g. `datavis.md`
- Add text to explain the purpose of the tutorial and what the code does
- Add images and links as suitable (you can use html code within Markdown)

Don't worry if you've never used Atom or Markdown before - we have created a template you can open straight in Atom and just insert your text, comments and images.

#### Open the file `md_template.md` in Atom. We have prepared a few sample topics based on which you can write a brief tutorial. Please choose a topic by clicking on it, which will take you to all the files necessary to write the tutorial.

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
                            <center><p>Traits along environmental gradients</p></center>
                          </div>
                        </div>
                      </a>
                  </li>
									<li>
										<a href="#density_maps">
											<img src="{{ site.baseurl }}/img/portfolio/density_rs_icon.png" alt="">
											<div class="overly">
												<div class="position-center">
													<center><h2>Visualising forest plot tree data</h2></center>
													<center><p>Traits along environmental gradients</p></center>
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
                </ul>
              </div>
            </div>
          </div>
        </div>
    </div>
</section>

<a name="polar_map"></a>

# Mapping species occurrence records

__The aims of this tutorial are to download species occurrence data from GBIF using the `rgbif` package, and then plot the data. We will also learn how to create a map with a top-down view of the world, as the species we've chosen, Arctic fox, is found in the Northern hemisphere.__

<center> <img src="{{ site.baseurl }}/img/fox_map.png" alt="Img" style="width: 500px;"/>   <img src="{{ site.baseurl }}/img/fox_map2.png" alt="Img" style="width: 500px;"/></center>
<center>Arctic fox occurrences based on available data from the Global Biodiversity Information Facility (GBIF).</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script is the `arctic_map.R` file in the `arctic_fox` folder.


<a name="forest_plots"></a>

# Visualising forest plot tree data

__This tutorial involves plotting tree inventory data from 2 permanent survey plots in a dry tropical savannah to see how tree morphology and spatial clustering of trees varies according to elephant activity.__

This tutorial should cover the basics of using the `ggplot2` package, using multiple layered visualisation methods to show variation in tree growth and morphology over space. Data visualisation will be complemented by a few boxplots. In addition, the tutorial will touch on  simple skills in the immensely popular `dplyr` package to prepare datasets for use in data visualisation.

<center> <img src="{{ site.baseurl }}/img/elephant_plot.png" alt="Img" style="width: 500px;"/>   <img src="{{ site.baseurl }}/img/no_elephant_plot.png" alt="Img" style="width: 500px;"/></center>
<center>Tree morphology and spatial clustering of trees in a plot with elephant activity (left) and without elephant activity (right).</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The data and script for this tutorial are in the `savanna_elephants` folder.


<a name="density_maps"></a>

# Density maps of red squirrel occurrences

__The tutorial will take you through the steps of downloading red squirrel occurrences in the UK from the Global Biodiversity Information Facility (GBIF), adjusting spatial projections and plot density maps with `ggplot2`.__

<center> <img src="{{ site.baseurl }}/img/density_rs.png" alt="Img" style="width: 600px;"/> </center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script for this tutorial `density_maps.R` is in the `density_maps` folder.


<a name="temp_timeseries"></a>

# Visualising temperature timeseries data

__The aim of this tutorial is to produce a line graph or time series plot with mean daily temperature plus errors using `ggplot2`, and similarly, to produce a second graph of daily temperature fluctuations using a smoother function. Finally, we will plot and save the two figures together using the `gridExtra` package.__

<center> <img src="{{ site.baseurl }}/img/temp_timeseries.png" alt="Img" style="width: 600px;"/> </center>
<center>Mean daily temperatures ± SD (left) and daily temperature fluctions in 2016.</center>



<a name="publish"></a>

*text on how to make a github pages repo and upload your md file there will appear here soon*


## Anders Kolstad

“The aim of this exercise is to produce a line graph or time series plot with mean daily temperature
plus errors using ggplot2, and similarly to produce a second graph of daily temperature
fluctuations using a smoother function. Finally, we plot and save the two figures together.

## Stefano Masier

Title: "Analysis of spatial movement"
Summary: the aim of this tutorial is to be able to visualize data from a series of geographical coordinates, plot them and extract some basic information.
The aim is to become able handle a series of coordinates, plot the path itself, but also calculate and plot the covered distance, the relative movement and the relative angle for each time step.
These info can then be used as a starting point to more advanced statistical analysis (i.e. GLMs)

It's an actual analysis that I run some time ago: there is a small loop to prepare the dataset for the modelling, but the people attending don't have to go through it unless we have time and they really want to.
The last part are just some models that I made: this part can be expanded or dropped, as you see fit.


## Dries Landuyt
title: Analysing leaf-level understorey photosynthesis within sunflecks
summary: In this tutorial, we learn to work with pipes and other dplyr functions and different plotting techniques using the ggplot2 package. We will apply these functionalities to explore the importance of sunflecks for carbon assimilation in an understorey herb based on a LICOR dataset (leaf-level gas exchange measurements) with a temporal resolution of 5 seconds, gathered on a sunny day in June 2017.



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
