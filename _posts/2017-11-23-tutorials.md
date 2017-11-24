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

### Find out for yourself - complete a quick Coding Club tutorial


#### To get a taste of the Coding Club experience, you can complete a <a href="https://ourcodingclub.github.io/2017/11/11/popchange.html" target="_blank">Coding Club tutorial on mapping vertebrate population change across Europe.</a>

<center><img src="{{ site.baseurl }}/img/anseriformes.png" alt="Img" style="width: 700px;"/></center>
<center><p><i>Anseriformes</i> populations in Europe.</p></center>


<a name="tutorial"></a>

### Write your own tutorial

__Next we will learn how to write, format and publish coding tutorials.__

We write our tutorials in Markdown and we use the Atom text editor, which is user-friendly text editor and easy on the eyes. You can use another text editor, like Brackets, if you prefer, the principle is the same. __You can <a href="https://atom.io/" target="_blank">download Atom here.</a>__

<center><img src="{{ site.baseurl }}/img/atom_screen.png" alt="Img" style="width: 700px;"/></center>


Our workflow tends to go like this:

#### - Write the `R` code for the tutorial in `RStudio`

#### - Save any graphs you create with your code

#### - Open `Atom`, copy and paste your `R` code in a new file

#### - Save the file as a `.md` file, e.g. `datavis.md`

#### - Add text to explain the purpose of the tutorial and what the code does

#### - Add images and links as suitable


#### Don't worry if you've never used `Atom` or `Markdown` before - we have created a template you can open straight in Atom and just insert your text, comments and images.


__You can download the  `tut_template.md` file that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them.__

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

## Mapping species occurrence records
#### By Gergana Daskalova

__The aims of this tutorial are to download species occurrence data from GBIF using the `rgbif` package, and then plot the data. We will also learn how to create a map with a top-down view of the world, as the species we've chosen, Arctic fox, is found in the Northern hemisphere.__

<center> <img src="{{ site.baseurl }}/img/fox_map.png" alt="Img" style="width: 500px;"/>   <img src="{{ site.baseurl }}/img/fox_map2.png" alt="Img" style="width: 500px;"/></center>
<center>Arctic fox occurrences based on available data from the Global Biodiversity Information Facility (GBIF).</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script is the `arctic_map.R` file in the `arctic_fox` folder.


<a name="forest_plots"></a>

## Visualising forest plot tree data
#### By John Godlee

__This tutorial involves plotting tree inventory data from 2 permanent survey plots in a dry tropical savannah to see how spatial clustering of trees varies according to elephant activity. The tutorial covers the basics of using the `ggplot2` package, using multiple layered visualisation methods to show variation in tree abundance over space. In addition, the tutorial will touch on  simple skills in the immensely popular `dplyr` package to prepare datasets for use in data visualisation.__

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

<center> <img src="{{ site.baseurl }}/img/temp_timeseries.png" alt="Img" style="width: 600px;"/> </center>
<center>Mean daily temperatures ± SD (left) and daily temperature fluctuations in 2016.</center>

#### You can download the `R` script that you can turn into a tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them. The script for this tutorial `temp_time_series.R` is in the `temp_timeseries` folder.


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

__Now you can see your new repository. Click on `Upload files` and upload your filled in `Markdown` template. To make our tutorial the landing (home) page of the website, we have to rename it to `index.md`. Click on the file you just uploaded, select `Edit` and change the filename. Remember to include the file extension as well, e.g. `index.md`. Upload any images you are using in your tutorial as well.__

You are two clicks away from having a website with your tutorial! Now click on `Settings` and scroll down to the `GitHub pages` section - we need to enable the `GitHub pages` feature, which turns our `index.md` file into a page, i.e. website. Change `Source` from `None` to `master` - the master branch of our repository. Click on `Save`.

<center> <img src="{{ site.baseurl }}/img/github_pages.png" alt="Img" style="width: 600px;"/> </center>

#### Congratulations, your repository is now published as a website!

__Scroll down to the `GitHub pages` section again - you can see the link for your tutorial! If you need to edit your tutorial, you can go back to your repository, select the `index.md` file, then click on `Edit` and make any necessary changes. You can also check out different themes for your website, though the default one is clean and tidy, which works well for coding and statistics tutorials in general.__

### We would love to see your tutorials - feel free to share them with us on Twitter __@our_codingclub__ or via email __ourcodingclub@gmail.com__

### Contribute a tutorial

__Are you keen to share some of your coding and statistics knowledge? We would love to have more people join our team and build a world-wide community of people teaching and learning together! You can take a look at the tutorials we have already developed - feel free to make suggestions for changes on existing tutorials and get in touch with us at ourcodingclub@gmail.com if you would like to make a new tutorial.__


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
