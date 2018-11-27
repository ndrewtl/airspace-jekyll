---
layout: post
title: Intro to the Google Earth Engine
subtitle: Quantifying forest cover change & harnessing the power of the Earth Engine to answer research questions
date: 2018-11-26 10:00:00
author: Gergana and Isla
meta: "Tutorials"
tags: modelling data_manip data_vis
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheader_gee.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#intro"> 1. Learn what is the Google Earth Engine </a>
#### <a href="#analyses"> 2. Find out what types of analyses you can do using the GEE </a>
#### <a href="#layout"> 3. Get familiar with the GEE layout </a>
#### <a href="#javascript"> 4. Learn the basic principles of JavaScript </a>
#### <a href="#import"> 5. Import and explore data - forest cover change as a case study </a>
#### <a href="#visualise"> 6. Visualise forest cover change </a>
#### <a href="#calculate"> 7. Calculate forest cover change over time in specific locations</a>
#### <a href="#export"> 8. Export results - summary tables </a>
#### <a href="#R"> 9. Further analysis and visualisation in R - the best of both worlds! </a>

### All the files you need to complete this tutorial will be generated and exported from the GEE during the course of the tutorial.

### <a href="https://signup.earthengine.google.com/" target="_blank">Follow this link</a> to register for the Google Earth Engine - it is free. 
__Say what you'll be using the GEE for - for research, education, etc. It might take a few hours or a day or so for your registration to be approved.__

<a name="intro"></a>

## 1. Learn what is the Google Earth Engine

The Google Earth Engine, as its developers have described it, is "_the most advanced cloud-based geospatial processing platform in the world!_" What this means is that through the Google Earth Engine, you can access and efficiently analyse numerous open-source spatial databases (like Landsat and MODIS remote sensing imagery, the Global Forest Change dataset, roads, protected areas, etc.). When doing these analyses, you are using the Google servers, so you can do analyses that would take weeks, if not months, on your computer or even a fancy computer.

__From the Google Earth Engine, you can export `.csv` files of any values you've calculated, `geoTIFF` files (georeferenced images) to your Google Drive account.__

<a name="analyses"></a>

## 2. Find out what types of analyses you can do using the GEE

__With the GEE, you can answer large-scale research questions in an efficient way that really was just not possible before, so quite exciting! You can use large geospatial datasets to address a plethora of questions and challenges facing humanity in the modern world. We will see later on how to explore what datasets are available to work with in the GEE, and it's also possible to import your own georeferenced imagery (like photos from drone missions).__ You can find out how to import your own raster data from <a href="https://developers.google.com/earth-engine/image_upload" target="_blank">this page</a> on the GEE developers website.

For example, you can classify different land cover types, you can calculate and extract values for landscape features such as <a href="https://en.wikipedia.org/wiki/Normalized_difference_vegetation_index" target="_blank">NDVI</a> (Normalised Difference Vegetation Index) - for the world, a particular region of interest, or many different areas around the world. Really, the possibilities are enormous, and here we are only scratching the surface by giving you an example of how you can use the GEE to calculate changes in forest cover over time.

### You can check out the tutorials on the <a href="https://developers.google.com/earth-engine/" target="_blank">Google Earth Engine Developers website</a> if you are keen to learn more and to practice your GEE skills!

<a name="layout"></a>

## 3. Get familiar with the GEE layout

### <a href="https://code.earthengine.google.com" target="_blank">Go to the Earth Engine to start your GEE journey!</a>

_Take a moment to familiarise yourself with the layout of the Earth Engine editor - like when first starting to learn a new language, it can seem like a lot to take in at once! With your blank script, have a go at exploring the different tabs. Notice how if you draw polygons or drop points, they will appear in your script. You can go to the `Inspector` tab, click on a place in the map, and see what information is available for it. Here is an outline of what most of the tabs do:_

<center> <img src="{{ site.baseurl }}/img/gee_layout.png" alt="Img" style="width: 900px;"/> </center>

<a name="javascript"></a>

## 4. Learn the basic principles of JavaScript

__The Google Earth Engine uses the programming language <a href="https://en.wikipedia.org/wiki/JavaScript" target="_blank">JavaScript.</a>__

We'll introduce you to more about `JavaScript` syntax and functions as we go along with the tutorial, but for now, here a few notes: 

Lines of code in `JavaScript` finish with a `;` - note that code for e.g. defining a variable can be spread over multiple lines, but you only need to put a `;` at the end of the last line of the code chunk.

To define new variables, you use:

```javascript
var new_variable = ...
```

You'll see variants of this code at multiple places throughout the script we will create later. Essentially, when you import datasets, create new layers, calculate new values, all those need to be stored as varibles so that you can map them, export them, etc.

To add comments in your script, use `//`, for example at the start of your blank new script (if you created any polygons or points while you were exploring, you can make a new script now to start "clean". Like when coding in other programming languages, it's great to leave comments to make sure your script outlines who you are, what the aim of the script is and why you are following the specific workflow. Here are a few example comments, you can write up something similar in your script:

```javascript
// Calculating forest cover change in protected areas around the world
// Gergana Daskalova
// 26th Nov 2018
```

__In JavaScript you have to run your entire script at once - that is, you can't for example select two lines of your script and run just those, you have to run the whole thing. You "run" a script by pressing the `Run` button. This means that throughout your tutorial, as you add more lines to your script, you have to keep pressing `Run` to see the results of the new code you've added.

<a name="import"></a>

## 5. Import and explore data - protected areas and forest cover change as a case study

Like with any analysis, it's not so much about the data as it is about your research question - so as you start exploring the GEE, remember to keep your research questions (or science communication goals, since the GEE is pretty great for that, too) in mind!

### Research question
__How has forest cover changed in different national parks around the world?__

### Import and explore a dataset in the GEE - protected areas

To import the protected area dataset (polygons of the protected areas around the world from the World Database of Protected Areas), type `protected area` in the search tab and select the polygon version of the database (the other one is just points, i.e. the coordinates of one point within the protected areas, not their outline).

<center> <img src="{{ site.baseurl }}/img/gee_import.png" alt="Img" style="width: 800px;"/> </center>

First, you'll see a pop window with some information about the dataset - the different types of information represented, the year it was created, etc. You can also practice searching for other types of data that come to your mind to see if they are available from the GEE.

__Select `Import`.__

Your imported dataset appears at the top of the script - it's currently called `table` which is not particularly informative, so you can rename that something else, e.g., `parks`.

<center> <img src="{{ site.baseurl }}/img/new_script.png" alt="Img" style="width: 800px;"/> </center>

__Remember to save your script, and to save it often! Once you've saved it, you'll see the file appear on the left under your scripts tab.__

### Visualise protected areas around the world

Next up, we'll use the `Map` function to map the dataset and we will add a layer - you can then turn that layer on and off from the layer tab in the top right corner of the map window. You can also change the opacity.

```javascript
// If you want to visualise the PAs around the world, you can use:
Map.addLayer(parks);
// Takes a while to load! Remember you need to press "Run" to see the results.
```

__Go to the `Inspector` tab, click on a point somewhere on the map and check out the `features` of that point - the name of the protected area, its area, when it was established, etc.__

#### Move around the world, find a national park and "inspect" it - can you find the name, area, etc. - all this information is under the `Inspector` tab.

<center> <img src="{{ site.baseurl }}/img/map_inspect.png" alt="Img" style="width: 800px;"/> </center>

### Import and explore a dataset in the GEE - forest cover change

Similarly to how you imported the protected area dataset, go to the search tab, type in `global forest change` and select the <a href="http://science.sciencemag.org/content/342/6160/850" target="_blank">Hansen et al. dataset</a>. 

Take a look at the different types of information held within this dataset - that will help you familiarise yourself with what to expect from our analyses later on.

<center> <img src="{{ site.baseurl }}/img/hansen_data.png" alt="Img" style="width: 800px;"/> </center>

__Call the object `gfc`, or whatever else you wish, but remember that if you call it something else, you have to change `gfc` to your new name in all the code coming up! Next up, we will again map our dataset.__

```javascript
// Add the Global Forest Change dataset
Map.addLayer(gfc);
```

<center> <img src="{{ site.baseurl }}/img/map_hansen.png" alt="Img" style="width: 800px;"/> </center>

Currently we just have a black and red map - black for the places where there are no forests, and red from the places that do have forest cover. This is not terribly informative and over the course of the tutorial we will work on making this map better!

__Go to the `Inspector` tab again, click on a point somewhere on the red parts map and check out the `features` of the forest cover change layer. If it says `loss: 0`, `gain: 0`, that means that in this specific pixel, no forest loss or gain has occurred.__

You can also turn layers on and off, and you can "comment out" certain parts of the code, if you don't want that action to be performed every single time you rerun the script. For example, mapping the protected area dataset takes quite a while - so if you didn't want to do that multiple times, you can add `//` in front of that line of code, and you can always remove the `//` when you do wish to map those data again. Like this:

```javascript
// If you want to visualise the PAs around the world, you can use:
// Map.addLayer(parks);
```

__If you want to turn lots of code lines into comments or turn lots of comments back into code, you can use a keyboard shortcut `Cmd + /` on a `Mac` and `Ctrl + /` on a `Windows` computer.__

We are now ready to improve our map and derive quantitative values for forest loss and gain!
<a name="visualise"></a>

## 6. Visualise forest cover change

First, it's good practice to define the scale of your analyses - in our case, it's 30 m, the resolution of the Global Forest Change dataset. If a given pixel has experienced forest loss, this means that somewhere in that 30 m x 30 m square, there were decreases in forest cover.

You can also set the scale to automatically detect the resolution of the dataset and use that as your scale.

Type up the following code in your script:

```javascript
// Set the scale for our calculations to the scale of the Hansen dataset
// which is 30m
var scale = gfc.projection().nominalScale();
```

__The next step is to create variables for the tree cover in 2000 (when the database starts), for the loss up until 2016 and the gain in forest cover, again up until 2016. In raster data, images usually have different "bands" (e.g., red, green, UV), and we can select which bands we want to work with. In this case, the different bands of the `gfc` object represent the forest cover, forest loss and forest gain, so we will make a variable for each.__

__To do this, we will use the `select()` function. Note that unlike other programming languages like `R`, in `JavaScript` you put the object you want to apply the function to first, and then the actual functin comes second.__

```javascript
// Create a variable for the original tree cover in 2000
var treeCover = gfc.select(['treecover2000']);

// Convert the tree cover layer because the treeCover by default is in
// hundreds of hectares, but the loss and gain layers are just in hectares!
treeCover = treeCover.divide(100);

// Create a variable for forest loss
var loss = gfc.select(['loss']);

// Create a variable for forest gain
var gain = gfc.select(['gain']);
```

### Make a global map of forest cover, forest loss and forest gain

Now that we have our three variables, we can create a layer for each of them and we can plot them using colours of our choice. We will use the same `Map.addLayer` function as before, but in addition to adding the object name, we will specify the colours and what we want to call the specific layers.

_Note that we are also introducing a new function `updateMask()` - what this does is mark the areas there was no forest cover in the year 2000 - they become transparent, so instead of just blackness, we can see the seas, rivers, continent outlines, etc._

```javascript
// Add the tree cover layer in light grey
Map.addLayer(treeCover.updateMask(treeCover),
    {palette: ['D0D0D0', '00FF00'], max: 100}, 'Forest Cover');

// Add the loss layer in pink
Map.addLayer(loss.updateMask(loss),
            {palette: ['#BF619D']}, 'Loss');

// Add the gain layer in yellow
Map.addLayer(gain.updateMask(gain),
            {palette: ['#CE9E5D']}, 'Gain');
```

Remember to click on `Run` so that you see your newly plotted maps. The forest layers might be easier to see if you either turn off the first two layers you plotted (the protected areas and the generic GFC layer). Or you can keep the protected area layer on, but reduce the opacity by dragging the bar below that layer.

<center> <img src="{{ site.baseurl }}/img/hansen_trio.png" alt="Img" style="width: 800px;"/> </center>

You can specify colour using hex codes, those are the number and letter combinations in the code above, e.g. `#CE9E5D` is yellwow. You can find examples of those online, for example <a href="https://htmlcolorcodes.com" target="_blank">this website</a>.

<center> <img src="{{ site.baseurl }}/img/colours_hex.png" alt="Img" style="width: 500px;"/> </center>

_You can also switch between map view and satellite view. If you zoom in enough and go to satellite view, you can actually start spotting some patterns, like forest loss along roads in the Amazon._

<center> <img src="{{ site.baseurl }}/img/amazon_forest.png" alt="Img" style="width: 800px;"/> </center>

<a name="calculate"></a>

## 7. Calculate total forest cover gain and loss in specific locations

__So far we can see where forest loss and gain have occurred, so we know about the _extent_ of forest change, but we don't know about the _magnitude_ of forest change, so our next step is to convert the number of pixels that have experienced gain or loss (remember that they are just 0 or 1 values, 0 for no, 1 for yes) into areas, e.g. square kilometers.__

For each of the 

```javascript
// The units of the variables are numbers of pixels
// Here we are converting the pixels into actual area
// Dividing by 10 000 so that the final result is in km2
var areaCover = treeCover.multiply(ee.Image.pixelArea())
                .divide(10000).select([0],["areacover"]);

var areaLoss = loss.gt(0).multiply(ee.Image.pixelArea()).multiply(treeCover)
              .divide(10000).select([0],["arealoss"]);

var areaGain = gain.gt(0).multiply(ee.Image.pixelArea()).multiply(treeCover)
              .divide(10000).select([0],["areagain"]);
```

<a name="export"></a>

## 8. Export results - summary tables


<a name="R"></a>

## 9. Further analysis and visualisation in R - the best of both worlds!




<hr>
<hr>

__Check out <a href="https://ourcodingclub.github.io/workshop/" target="_blank">this page</a> to learn how you can get involved! We are very happy to have people use our tutorials and adapt them to their needs. We are also very keen to expand the content on the website, so feel free to get in touch if you'd like to write a tutorial!__

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/). <a href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://licensebuttons.net/l/by-sa/4.0/80x15.png" alt="Img" style="width: 100px;"/></a>

<h3><a href="https://www.surveymonkey.co.uk/r/PFJ7S2D" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>

<br>
<h3>&nbsp; You can contact us with any questions on <a href="mailto:ourcodingclub@gmail.com?Subject=Tutorial%20question" target = "_top">ourcodingclub@gmail.com</a></h3>
<br>
<h3>&nbsp; Related tutorials:</h3>

{% assign posts_thresh = 8 %}

<ul>
  {% assign related_post_count = 0 %}
  {% for post in site.posts %}
    {% if related_post_count == posts_thresh %}
      {% break %}
    {% endif %}
    {% for tag in post.tags %}
      {% if page.tags contains tag %}
        <li>
            <a href="{{ site.url }}{{ post.url }}">
	    &nbsp; - {{ post.title }}
            </a>
        </li>
        {% assign related_post_count = related_post_count | plus: 1 %}
        {% break %}
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>

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
