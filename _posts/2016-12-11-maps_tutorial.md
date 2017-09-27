---
layout: post
title: Spatial Data and Maps
subtitle: Using R as a GIS software tool and creating informative maps
date: 2016-12-11T16:00:00.000Z
author: John
meta: Maps_1
tags: datavis
---

<div class="block">
  <center>
  <img src="{{ site.baseurl }}/img/tutheader_maps.jpg" alt="Img">
</center>
</div>

# Tutorial Aims:

#### 1. Learn to download map tiles using ggmap

#### 2. Make a simple map using ggmap

#### 3. Import, manipulate and plot shapefiles

# Steps:

#### <a href="#why">1. Why use R to make maps?</a>

#### <a href="#download">2. Downloading the relevant packages</a>

#### <a href="#map_data">3. Getting your head around map data</a>

#### <a href="#create">4. Creating a map using ggmap</a>

#### <a href="#shp">5. Using shapefiles</a>


--------------------------------------------------------------------------------
Open up a new R Script where you will be adding the code for your maps. All the resources for this tutorial, including some helpful cheatsheets can be downloaded from [this repository](https://github.com/ourcodingclub/CC-6-Maps) Clone and download the repo as a zipfile, then unzip and set the folder as your working directory by running the code below (subbing in the actual folder path), or clicking `Session/ Set Working Directory/ Choose Directory` from the RStudio menu.

```r
setwd("PATH_TO_FOLDER")
```

<a name="why"></a>

## Why use R for spatial data?

##### __Less clicking:__
  - Most conventional GIS software use a Graphical User Interface (GUI) which makes them easier to fumble through when you don't know what you're doing, but point and click interfaces become very laborious when performing analyses for the _n_ th time or when you really know your way around the software. R runs using a Command Line Interface, so while there may be more of a learning curve to begin with, it's pretty sweet once you know what to do.

##### __Reproducible analyses with new data:__
  - Imagine you have a data project where you are given new data every week, which you want compare using maps. Using a GUI, you would have to repeat your analyses step by step, every time your data came in, being careful to maintain formatting between maps. Using the command line in R, you only have to plug in the new data to the script and the maps will look the same every time.

##### __Free:__
  - While ArcGIS and SuperGIS cost money to use, R packages are free and probably always will be.

##### __A range of GIS packages for different applications:__
  - Using the R package system you can find the right GIS application for your project, and you can adapt and hack the packages already there to create something specific for your project.

<a name="download"></a>

## Downloading the relevant packages

Install the following packages:

```r
install.packages("readr") # Read in files
install.packages("dplyr") # Formatting data
install.packages("rgdal") # Manipulate map data
install.packages("devtools")

library(readr)
library(dplyr)
library(rgdal)
library(devtools)
  devtools::install_github("dkahle/ggmap") # Plot map data, download map tiles from online sources
    library(ggmap)
```


At the time of writing, `ggmap` needs to be compiled from source (i.e. its repository on Github) to maintain some functionality, hence `  devtools::install_github("dkahle/ggmap")`, but this might change in the future.

<a name="map_data"></a>

## Getting your head around map data

The easiest way to think about map data is to first imagine a graph displaying whatever data you want, but with the x and y axes denoting longitude and latitude:

<center><img src="{{ site.baseurl }}/img/Trout_Europe_Plot.jpeg" alt="Img" style="width: 700px;"/></center>

Then it's a simple case of adding a background map to your image to place the data points in the real world. In this case, the map was pulled from google maps using the `ggmap` package.

<center><img src="{{ site.baseurl }}/img/Trout_Europe_Map.jpeg" alt="Img" style="width: 700px;"/></center>

That was a simple example, and maps can incorporate more complex elements like polygons and lines:

<center><img src="{{ site.baseurl }}/img/Polygon_Line_Map.jpeg" alt="Img" style="width: 700px;"/></center>

<a name="create"></a>

## Creating a map using ggmap

For this part of the tutorial we are going to create a map showing the spatial extent of 2 species of bird.  Rueppell's Vulture (_Gyps rueppellii_) feeds on large mammalian carrion and the African Penguin (_Spheniscus demersus_) feeds on small marine fish, it's probable that they have distinct spatial patterns, we shall see! We will use species occurence data from the <a href="http://www.gbif.org/" target="_blank">Global Biodiversity Information Facility (GBIF)</a>, which you have already downloaded and unzipped from [the repository](https://github.com/ourcodingclub/CC-6-Maps) for this tutorial.

First, import the data we need, `Gyps_rueppellii_GBIF.csv` and `Spheniscus_dermersus_GBIF.csv`:

```r
vulture <- read.csv("Gyps_rueppellii_GBIF.csv", sep="\t")
penguin <- read.csv("Spheniscus_dermersus_GBIF.csv", sep="\t")
```

Now onto cleaning up the data using `dplyr`. If you are keen to learn more about using the `dplyr` package, check out our [tutorial on data formatting and manipulation](https://ourcodingclub.github.io/2017/01/16/piping.html).

```r
library(dplyr)

# Keep only the columns we need
vars <- c("gbifid", "scientificname", "locality", "decimallongitude", "decimallatitude", "coordinateuncertaintyinmeters")

vulture_trim <- vulture %>% select(one_of(vars)) # `one_of()` is part of `select()` and selects all columns specified in `vars`
penguin_trim <- penguin %>% select(one_of(vars))

# Combine the dataframes
pc_trim <- bind_rows(vulture_trim, penguin_trim)
str(pc_trim) # Check column names and content
# Check that species names are consistent
unique(pc_trim$scientificname)
  # Needs cleaning up

# Clean up "scientificname" to make names consistent
pc_trim$scientificname <- pc_trim$scientificname %>%
                            recode("Gyps rueppellii (A. E. Brehm, 1852)" = "Gyps rueppellii",
                              "Gyps rueppellii subsp. erlangeri Salvadori, 1908" = "Gyps rueppellii",
                              "Gyps rueppelli rueppelli" = "Gyps rueppellii",
                              "Spheniscus demersus (Linnaeus, 1758)" = "Spheniscus demersus"
                              )
# Checking names
unique(pc_trim$scientificname)
  # Done
```

Now we can make a preliminary plot to make sure the data looks right. Remember, a map is just a graph with longitude and latitude as the x and y axes:

```r
ggplot(pc_trim, aes(x = decimallongitude, y = decimallatitude, group = scientificname)) +
geom_point(aes(colour = scientificname))
```

It looks like some of the penguin populations might be from zoos in U.S cities, let's remove those entries:

```r
pc_trim <- pc_trim %>% filter(decimallongitude > -50)
```

Plot it again:

```r
ggplot(pc_trim, aes(x = decimallongitude, y = decimallatitude, group = scientificname)) + geom_point(aes(colour = scientificname))
```

Now to make a map out of our graph using `ggmap`, which pulls map tiles from various online sources, including google maps and open street maps.

First make a bounding box (`bbox`), to tell `ggmap` where to download map tiles from. The bounding box must be in the form of a vector, with decimal latitude and longitude values in this order `lowerleftlon, lowerleftlat, upperrightlon, upperrightlat`, which we can extract from our data frame using the following code:

```r
bbox <- c(min(pc_trim$decimallongitude) - 2,
          min(pc_trim$decimallatitude) - 2,
          max(pc_trim$decimallongitude) + 2,
          max(pc_trim$decimallatitude) + 2
          )
```

the `+2` `-2` values are added to make the edges of the map slightly larger than the limits of the data, purely for aesthetic reasons.

Now to download the map data from `ggmap`:

```r
Map_penguin <- get_map(location = bbox, source = "stamen", maptype = "terrain")
```

We can check that the map is correct by plotting the `Map_penguin` object:

```r
ggmap(Map_penguin)
```

To add the data, use `ggplot2` syntax:

```r
ggmap(Map_penguin) +
  geom_point(aes(x = decimallongitude,
                 y = decimallatitude,
                 colour = scientificname),
             data = pc_trim,
             alpha = 0.6,                     # `alpha=` sets the transparency of `geom_point()`, from 0 (transparent) to 1 (opaque)
             size = 2) +                      # `size=` sets the diameter of `geom_point()`
  scale_colour_manual(values=c("red", "blue")) +  # `scale_colour_manual()` sets the geom_point colours to specific values
  xlab(expression("Decimal Longitude ("*degree*")")) +  # Wrapping label in `expression()` and using *degree* lets us add a degree symbol
  ylab(expression("Decimal Latitude ("*degree*")"))
```

Now you should have a map that looks something like this:

<center><img src="{{ site.baseurl }}/img/Birds_ggmap.jpg" alt="Img" style="width: 700px;"/></center>

#### ggmap can access a whole load of different map types. Have a go at redoing the map above with some alternative map types by replacing the `source =` and `maptype =` arguments in `get_map()`:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-031e">`source =`</th>
    <th class="tg-031e"><b>google</b></th>
    <th class="tg-yw4l"><b>stamen</b></th>
    <th class="tg-yw4l"><b>osm</b></th>
  </tr>
  <tr>
    <td class="tg-031e" rowspan="11">`maptype =` </td>
    <td class="tg-031e">satellite</td>
    <td class="tg-yw4l">terrain</td>
    <td class="tg-yw4l">&lt;empty&gt;</td>
  </tr>
  <tr>
    <td class="tg-031e">terrain</td>
    <td class="tg-yw4l">terrain-background</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-031e">roadmap</td>
    <td class="tg-yw4l">terrain-labels</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">hybrid</td>
    <td class="tg-yw4l">terrain-lines</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">terrain</td>
    <td class="tg-yw4l">toner</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">terrain-background</td>
    <td class="tg-yw4l">toner-background</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><br></td>
    <td class="tg-yw4l">toner-hybrid</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><br></td>
    <td class="tg-yw4l">toner-labels</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><br></td>
    <td class="tg-yw4l">toner-lines</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><br></td>
    <td class="tg-yw4l">toner-lite</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><br></td>
    <td class="tg-yw4l">watercolor</td>
    <td class="tg-yw4l"></td>
  </tr>
</table>

<center>
	<img src="{{ site.baseurl }}/img/Map_collage.png" alt="Img" style="width: 700px;"/>
</center>

<a name="shp"></a>

## Using shapefiles
Shapefiles are a data format developed by [ESRI](http://www.esri.com) used to hold information on spatial objects. Despite the name, a shapefile consists of a few different files:

__Mandatory files:__

.shp = The main file containing the geometry data

.shx = An index file

.dbf = An attribute file holding information on each object

__Additional files:__

.prj = A file containing information on the Co-ordinate Reference system

.shp.xml = a file containing object metadata, citations for data, etc.

__And many more!__

We are going to use a shapefile of the World's Freshwater Ecoregions provided by [The Nature Conservancy](http://www.feow.org) to investigate the range of the Brown Trout in Europe using data from the [GBIF database](http://www.gbif.org).

Read in the GBIF data:

```r
Brown_Trout <- read.csv("Brown_Trout_GBIF_clip.csv")
```

Let's check that the data is displaying correctly using `ggplot()` like in the previous example:

```r
ggplot(Brown_Trout, mapping = aes(x = decimallongitude, y = decimallatitude)) + geom_point(alpha = 0.5)
```
We can roughly see the outline of Scandinavia and maybe the Northern Mediterranean.

Again, to plot our map, first make a bounding box, then download the map tiles using `ggmap`. We can set the map colour to greyscale with `color = "bw"`, so our shapefiles stand out. We can also set the map zoom with `zoom = 3`, with 3 being continent scale and 21 being individual buildings. This time we will make the bounding box manually:

```r
bbox <- c(-40, 30, 40, 85)
Map_trout <- get_map(location = bbox, source = "google", maptype = "terrain", zoom = 3, color = "bw")
```

Then we can plot the map tiles with the data using `ggmap()`:

```r
ggmap(Map_trout) +
  geom_point(colour = "blue", alpha = 0.5,
             aes(x = decimallongitude, y = decimallatitude),
             data = Brown_Trout) +
  theme_bw() +
  xlab("Longitude") +
  ylab("Latitude")
```

Now to read in the shapefiles. `readOGR()` converts a shapefile into a spatial object that can be interpreted by `ggmap`. `dsn = "FEOW-TNC"` gives the name of the folder where the shapefile can be found, `layer = "FEOWv1_TNC"` gives the name of the files to read in. It's important to keep filenames identical in a shapefile:

```r
shpData_FEOW <- readOGR(dsn = "FEOW-TNC", layer = "FEOWv1_TNC")
```

Now we have to check that the shapefile has the right Co-ordinate Reference System (CRS) to be read by `ggmap`. A CRS specifies how the coordinates of the 2D map displayed on the computer screen are related to the real globe, which is roughly spherical. There are lot's of different CRSs, used for maps of different scales, or of different parts of the globe (e.g. the poles) and it is important to keep them consistent amongst all the elements of your map For more information on CRSs have a look at "Coord_Ref_Systems.pdf" in [the repository](https://github.com/ourcodingclub/CC-6-Maps) :

```r
proj4string(shpData_FEOW)
```

To transform the CRS to the correct one we can use `spTransform` by specifying the correct CRS for `ggmap` which is [EPSG:WGS84](http://spatialreference.org/ref/epsg/wgs-84/) (`+proj=longlat +datum=WGS84`), then restructure the object into a data frame ready for plotting using `fortify()`:

```r
shpData_FEOW <- spTransform(shpData_FEOW, CRS("+proj=longlat +datum=WGS84"))
shpData_FEOW <- fortify(shpData_FEOW)
```

Now, plot the map, point data and shapefile together. The shapefiles can be plotted using `geom_map()`, specifying that the map (i.e. the shapes) and the data (i.e. the colours filling the shapes) both come from the shapefile, `color = black` makes the shape outlines black:

```r
Map_FEOW <- ggmap(Map_trout) +
  geom_map(data = shpData_FEOW,
           map = shpData_FEOW,
           aes(x = long, y = lat, map_id = id, group = group, fill = id),
           color = "black", size = 0.5) +
  geom_point(colour = "blue", alpha = 0.5, size = 0.5,
             aes(x = decimallongitude, y = decimallatitude),
             data = Brown_Trout) +
  theme(legend.position="none") +
  xlab("Longitude") +
  ylab("Latitude")

Map_FEOW
```

We can add extra elements using the `ggplot2` syntax, just like a normal `ggplot()`:

```r
Map_FEOW +
  annotate("rect", xmin = 20 , xmax = 35, ymin = 55, ymax = 65, fill="red", alpha=0.5) +
  annotate("text", x = 27.5, y = 61, label = "Restock") +
  annotate("text", x = 27.5, y = 59, label = "Area")
```

<hr>
<hr>

<h3><a href="https://www.surveymonkey.co.uk/r/F5PDDHV" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
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


