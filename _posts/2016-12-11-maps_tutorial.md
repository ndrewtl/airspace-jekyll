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

#### <a href="#create_map">4. Creating a map using `ggplot2` and `maps`</a>

#### <a href="#create_ggmap">5. Creating a map using `ggmap`</a>

#### <a href="#shp">6. Using shapefiles</a>

All the resources for this tutorial, including some helpful cheatsheets can be downloaded from <a href="https://github.com/ourcodingclub/CC-6-Maps" target="_blank">this Github repository</a>. Clone and download the repo as a zipfile, then unzip it.

Next, open up a new R Script where you will be adding the code for your mapsa. Set the folder you just downloaded as your working directory by running the code below (subbing in the location of the folder on your computer, e.g. `~/Downloads/CC-6-Maps-master`):

```r
setwd("PATH_TO_FOLDER")
```

<a name="why"></a>

## Why use R for spatial data?

##### __Less clicking:__
  - Most conventional GIS software use a Graphical User Interface (GUI) which makes them easier to fumble through when you don't know what you're doing, but point and click interfaces become very laborious when performing analyses for the _n_ th time or when you really know your way around the software. R runs using a Command Line Interface, so while there may be more of a learning curve to begin with, it's pretty sweet once you know what to do.

##### __Reproducible analyses with new data:__
  - Imagine you have a data project where you are given new data every week, which you want compare using maps. Using a GUI, you would have to repeat your analyses step by step, every time your data came in, being careful to maintain formatting between maps. Using the command line in R, you only have to plug in the new data to the script and the maps will look the same every time.

##### __It's free:__
  - While ArCGIS and SuperGIS cost money to use, R packages are free and probably always will be.

##### __A range of GIS packages for different applications:__
  - Using the R package system you can find the right GIS application for your project, and you can adapt and hack the packages already there to create something specific for your project.

<a name="download"></a>

## Downloading the relevant packages

Load the following packages, remember if you haven't installed the packages first, you will have to use `install.packages("PACKAGE_NAME")` first:

```r
library(readr)  # For reading in files
library(dplyr)  # For formatting and cleaning data
library(rgdal)  # For manipulating map data
library(raster)  # For clipping shapefile polygons
library(ggplot2)  # For drawing plots
library(maps)  # For making maps
library(mapdata)  # For supplying map data
library(gpclib)  # For clipping polygons
library(maptools) # For reading map data
library(rtools)  # Not bundled with R as standard anymore
library(devtools)  # For installing packages from altenative sources, e.g. Github
	devtools::install_github("dkahle/ggmap")
	devtools::install_github("oswaldosantos/ggsn")
library(ggmap)  # For plotting map data, downloading map tiles from online sources
library(ggsn)  # For adding scalebars and north arrows.
```

At the time of writing, `ggmap` and `ggsn` need to be compiled from source (i.e. their repositories on Github) to maintain some functionality, hence `devtools::install_github("")`, but this will hopefully change in the future when the updated versions of the packages are uploaded to CRAN.

Also, you should the following line after loading all your packages to allow `maptools` to use the `gpclib` package:

```r
gpclibPermit()
```

Also note that if you are on Linux, installing the `devtools` package may not work, throwing an error like `non-zero exit status`. Hopefully you can fix this by entering the following into your Linux terminal to install some dependencies, then reinstalling `devtools` in R. This was tested on Ubuntu 16.04.4 LTS in March 2018:

```shell
apt-get -y build-dep libcurl4-gnutls-dev
apt-get -y install libcurl4-gnutls-dev
```

<a name="map_data"></a>

## Getting your head around map data

The easiest way to think about map data is to first imagine a graph displaying whatever data you want, but where the x and y axes denote longitude and latitude instead of a variable:

<center><img src="{{ site.baseurl }}/img/Trout_Europe_Plot.jpeg" alt="Img" style="width: 700px;"/></center>

Then it's a simple case of adding a background map to your image to place the data points in the real world. In this case, the map was pulled from Google maps using the `ggmap` package.

<center><img src="{{ site.baseurl }}/img/Trout_Europe_Map.jpeg" alt="Img" style="width: 700px;"/></center>

That was a simple example, maps can incorporate more complex elements like polygons and lines, each with their own values:

<center><img src="{{ site.baseurl }}/img/map_FEOW_annot.png" alt="Img" style="width: 700px;"/></center>

<a name="create_map"></a>

## Creating a map using `ggplot2` and `maps`

For this part of the tutorial we are going to create a map showing occurrence records of 2 species of bird.  Rueppell's Vulture (_Gyps rueppellii_) feeds on large mammalian carrion and the African Penguin (_Spheniscus demersus_) feeds on small marine fish, it's probable that they have distinct spatial patterns, we shall see! We will use species occurence data from the <a href="http://www.gbif.org/" target="_blank">Global Biodiversity Information Facility (GBIF)</a>, which you have already downloaded from <a href="https://github.com/ourcodingclub/CC-6-Maps" target="_blank">the repository</a> for this tutorial.

First, import the data we need, `Gyps_rueppellii_GBIF.csv` and `Spheniscus_dermersus_GBIF.csv`:

```r
vulture <- read.csv("Gyps_rueppellii_GBIF.csv", sep="\t")
penguin <- read.csv("Spheniscus_dermersus_GBIF.csv", sep="\t")
```

Now onto cleaning up the data using `dplyr`. If you are keen to learn more about using the `dplyr` package, check out our <a href="https://ourcodingclub.github.io/2017/01/16/piping.html" target="_blank">tutorial on data formatting and manipulation</a>.

```r
# Keep only the columns we need
vars <- c("gbifid", "scientificname", "locality", "decimallongitude",
          "decimallatitude", "coordinateuncertaintyinmeters")

vulture_trim <- vulture %>% dplyr::select(one_of(vars))
penguin_trim <- penguin %>% dplyr::select(one_of(vars))
	# `one_of()` is part of `select()` and selects all columns specified in `vars`

# Combine the dataframes
pc_trim <- bind_rows(vulture_trim, penguin_trim)

# Check column names and content
str(pc_trim)

# Check that species names are consistent
unique(pc_trim$scientificname)
  # Needs cleaning up

# Clean up "scientificname" to make names consistent
pc_trim$scientificname <- pc_trim$scientificname %>%
                            recode("Gyps rueppellii (A. E. Brehm, 1852)" = "Gyps rueppellii",
                              "Gyps rueppellii subsp. erlangeri Salvadori, 1908" = "Gyps rueppellii",
                              "Gyps rueppelli rueppelli" = "Gyps rueppellii",
                              "Spheniscus demersus (Linnaeus, 1758)" = "Spheniscus demersus")

# Checking names
unique(pc_trim$scientificname)
  # Done
```

Now we can make a preliminary plot to make sure the data looks right. Remember, a map is just a graph with longitude and latitude as the x and y axes:

```r
ggplot(pc_trim, aes(x = decimallongitude, y = decimallatitude, colour = scientificname)) +
geom_point()
```

If you squint, you might be able to see the southern African cape, with lots of penguins on it. It looks like some of the penguin populations might be from zoos in U.S cities, but we only want to plot natural populations, so let's remove those entries:

```r
pc_trim_us <- pc_trim %>% filter(decimallongitude > -50)
```

Plot it again:

```r
ggplot(pc_trim_us, aes(x = decimallongitude, y = decimallatitude, colour = scientificname)) +
	geom_point()
```

Now we can add some simple map data from the `maps` package, which integrates nicely with `ggplot2`.

First we need to pull some map data:

```r
map_world <- borders("world", fill = "grey90", colour = "black")
```

Then you can plot `map_world` by simply adding it to your ggplot2 call and designating the `ggplot()` as a map using `coord_quickmap()`:

```r
ggplot() +
	map_world +  # Add world map
	geom_point(data = pc_trim_us,  # Add and plot species data
						 aes(x = decimallongitude, y = decimallatitude, colour = scientificname)) +
	coord_quickmap() +  # Define aspect ratio of the map, so it doesn't get stretched when resizing
	theme_classic() +  # Remove ugly grey background
	xlab("Longitude") +
	ylab("Latitude") + 
	guides(colour=guide_legend(title="Species"))
```

<center><img src="{{ site.baseurl }}/img/map_world_penguins.png" alt="Img" style="width: 700px;"/></center>

You can also subset the contents of `world_map`, to only plot a particular country or set of countries. Say we wanted to only plot the distribution of vultures and penguins in southern Africa, in the countries of South Africa, Namibia, Botswana, Zimbabwe. We can set the `region` argument of `borders()`:

```r
# Make a vector of country names
saf_countries <- c("South Africa", "Namibia", "Botswana", "Zimbabwe")

# Call the vector in `borders()`
map_saf <- borders("world", regions = saf_countries, fill = "grey90", colour = "black")
```

Then define the x and y axis limits in `ggplot()` using `xlim()` and `ylim()` with a bit of trial and error:

```r
ggplot() +
	map_saf +  # Add map
	geom_point(data = pc_trim_us,  # Add and plot speices data
						 aes(x = decimallongitude, y = decimallatitude, colour = scientificname)) +
	coord_quickmap() +  # Define aspect ratio of the map, so it doesn't get stretched when resizing
	xlim(8, 35) +  # Set x axis limits, xlim(min, max)
	ylim(-35, -15) +  # Set y axis limits
	theme_classic() +  # Remove ugly grey background
	theme(legend.position = "top") +  # Position the legend at the top of the plot
	xlab("Longitude") +
	ylab("Latitude") + 
	guides(colour=guide_legend(title="Species"))
	
```

<center><img src="{{ site.baseurl }}/img/map_saf_penguins.png" alt="Img" style="width: 800px;"/></center>

<a name="create_ggmap"></a>

## Creating a map using `ggplot2` + `ggmap`

The `ggmap` package also offers decent options for plotting maps. `ggmap` pulls map tiles as image files from various online sources, including Google maps and Open Street Maps.

First make a bounding box (`bbox`), to tell `ggmap` what region of the world to download map tiles for. The bounding box must be in the form of a vector, with decimal latitude and longitude values in this order `c(lowerleftlongitude, lowerleftlatitude, upperrightlongitude, upperrightlatitude)`. We can set the bounding box to the size of our data using the following:

```r
bbox <- c(min(pc_trim_us$decimallongitude) - 2,
          min(pc_trim_us$decimallatitude) - 2,
          max(pc_trim_us$decimallongitude) + 2,
          max(pc_trim_us$decimallatitude) + 2
          )
```

the `+2` `-2` values are added to make the edges of the map slightly larger than the limits of the data, purely for aesthetic reasons.

Now to download the map data from `ggmap`, using `bbox` in the `location` argument:

```r
map_penguin <- get_map(location = bbox, source = "stamen", maptype = "toner-lite")
```

We can check that the map is correct by plotting the `map_penguin` object:

```r
ggmap(map_penguin)
```

Note that sometimes `ggmap()` will fail, especially if you're internet connection is patchy. Try running it a few more times before looking for other fixes.

To add the data, use `ggplot2` syntax but define the base plot as a `ggmap()` instead of a `ggplot()`:


```r
ggmap(map_penguin) +
	geom_point(data = pc_trim_us,
	aes(x = decimallongitude,
		y = decimallatitude,
		colour = scientificname),
		alpha = 0.6,                     # `alpha=` sets the transparency of `geom_point()`, from 0 (transparent) to 1 (opaque)
		size = 2) +                      # `size=` sets the diameter of `geom_point()`
	xlab(expression("Decimal Longitude ("*degree*")")) +  # Wrapping the label in `expression()` and using *degree* lets us add a degree symbol
	ylab(expression("Decimal Latitude ("*degree*")"))
```

Now you should have a map that looks something like this:

<center><img src="{{ site.baseurl }}/img/penguin_toner.png" alt="Img" style="width: 700px;"/></center>

`ggmap` can access a whole load of different map types. Have a go at re-plotting the map above with some alternative map types by replacing the `source =` and `maptype =` arguments in `get_map()`. But be warned, not every maptype is available for the entire world:

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

`ggmap` can also be used to get detailed maps of local areas using the `zoom` argument. As a completely trivial exmaple, let's plot the distribution of <a href="http://data.edinburghopendata.info/dataset/play-areas" target="_blank">Council owned outdoor play areas in Edinburgh</a>:

Import the data:

```r
play_areas <- read.csv("play_areas.csv")
```

Plot the map:

```r
edi_map <- get_map(location = "Edinburgh", zoom = 12, source = "google", maptype = "hybrid")

ggmap(edi_map) +
	geom_point(data = play_areas, aes(x = long, y = lat), size = 4, colour = "#06BA00")
```

<a name="shp"></a>

## Using shapefiles

Shapefiles are a data format developed by [ESRI](http://www.esri.com) used to hold information on spatial objects. They are pretty ubiquitous and can be used by a lot of GIS packages Shapefiles can hold polygon, line or point data. Despite the name, a shapefile consists of a few different files:

__Mandatory files:__

`.shp` = The main file containing the geometry data

`.shx` = An index file

`.dbf` = An attribute file holding information on each object

__Additional files:__

`.prj` = A file containing information on the Coordinate Reference system

`.shp.xml` = a file containing object metadata, citations for data, etc.

__And many more!__

We are going to use a shapefile of the World's Freshwater Ecoregions provided by <a href="http://www.feow.org" target="_blank">The Nature Conservancy</a> to investigate the range of the Brown Trout in Europe using data from the <a href="http://www.gbif.org" target="_blank">GBIF database</a>.

Read in the GBIF data for the Brown Trout:

```r
brown_trout <- read.csv("Brown_Trout_GBIF_clip.csv")
```

Check that the data is displaying correctly using `ggplot()` like in the previous example:

```r
ggplot(brown_trout, mapping = aes(x = decimallongitude, y = decimallatitude)) + geom_point(alpha = 0.5)
```
We can roughly see the outline of Scandinavia and maybe the Northern Mediterranean if you squint.

Again, to plot a preliminary map, first make a bounding box for the extent of the map, then download the map tiles using `ggmap`. We can set the map colour to greyscale with `color = "bw"`, so our shapefiles stand out. We can also set the map zoom with `zoom = 3`, with 3 being continent scale and 21 being individual buildings. This time we will make the bounding box manually:

```r
bbox <- c(-40, 30, 40, 85)
Map_trout <- get_map(location = bbox, source = "google", maptype = "terrain", zoom = 3, color = "bw")
```

You'll get a warning message saying: "Warning: bounding box given to google - spatial extent only approximate..." - this is because we haven't specified a coordinate system, and instead are using the default. For our purposes, that's okay, so you can move on and not worry about this message.

Then we can plot the map tiles with the data using `ggmap()`:

```r
ggmap(Map_trout) +
  geom_point(colour = "blue", alpha = 0.5,
             aes(x = decimallongitude, y = decimallatitude),
             data = brown_trout) +
  theme_bw() +
  xlab("Longitude") +
  ylab("Latitude")
```

It looks like the brown trout data has been imported fine. But instead of using ggmap to draw map elements, in this example we're going to use our own shapefiles.

Now to read in the shapefiles. `readOGR()` converts a shapefile into a SpatialPolygons object that can be interpreted by R. `dsn = "FEOW-TNC"` gives the name of the folder where the shapefile can be found, `layer = "FEOWv1_TNC"` gives the name of the files to read in. It's important to keep filenames identical in a shapefile:

```r
shpData_FEOW <- readOGR(dsn = "FEOW-TNC", layer = "FEOWv1_TNC")
```

Now we have to check that the shapefile has the right Co-ordinate Reference System (CRS) to be read by `ggplot2`. A CRS specifies how the coordinates of the 2D map displayed on the computer screen are related to the real globe, which is roughly spherical. There are lot's of different CRSs, used for maps of different scales, or of different parts of the globe (e.g. the poles) and it is important to keep them consistent amongst all the elements of your map. You can use `proj4string()` to check the CRS. For more information on CRSs have a look at "Coord_Ref_Systems.pdf" in <a href="https://github.com/ourcodingclub/CC-6-Maps" target="_blank">the repository you downloaded earlier</a>:

```r
proj4string(shpData_FEOW)
```

To transform the CRS to the correct one for use with `ggplot2`, we can use `spTransform` and specify the correct CRS, which is <a href="http://spatialreference.org/ref/epsg/wgs-84/" target="_blank">EPSG:WGS84</a> (`+proj=longlat +datum=WGS84`):

```r
shpData_FEOW <- spTransform(shpData_FEOW, CRS("+proj=longlat +datum=WGS84"))
```

At this point I wouldn't recommend plotting `shpData_FEOW`, it's a pretty big file, but so you can get an idea of what it looks like:

<center><img src="{{ site.baseurl }}/img/ecoregions_global_map.png" alt="Img" style="width: 700px;"/></center>

The shapefile contains ecoregions for the entire world, but we only want to plot the ecoregions where the brown trout is found. You can crop SpatialPolygons objects to the size of a bounding box using `intersect()` from the `raster` package:

```r
clip_box <- as(extent(min(brown_trout$decimallongitude) -15,
	max(brown_trout$decimallongitude) + 10,
	min(brown_trout$decimallatitude),
	max(brown_trout$decimallatitude)), "SpatialPolygons")

shpdata_feow_clipped <- intersect(shpdata_feow, clip_box)
```

plot `shpdata_feow_clipped` to see that `intersect()` has cropped out polygons that were outside our bounding box, and has helpfully joined up the perimeters of any polygons that straddle the edge of the bounding box:

```r
plot(shpdata_feow_clipped)
```

<center><img src="{{ site.baseurl }}/img/ecoregions_clipped_map.png" alt="img" style="width: 700px;"/></center>

then we need to restructure the object into a data frame ready for plotting. the dataframe needs to contain the id for each polygon, in this case the name of the ecoregion it is from. explore the contents of `shpdata_feow_clipped`, using `str`. `@` accesses sub-dataframes within the `shpdata_feow` spatial object:

```r
str(shpData_FEOW_clipped@data)
```

`ECOREGION` contains all the data for the different types of ecoregions, they have names like "Aegean Drainages" and "Central Prairie". Now we can use `ECOREGION` as an identifier in the `fortify()` command to transform the spatial object to a dataframe, where each polygon will be given an `id` of which `ECOREGION` it is from:

```r
shpData_FEOW_clipped_fort <- fortify(shpData_FEOW_clipped, region = "ECOREGION")  # this could take a while
```

Now, plot the map, point data and shapefile together. The ecoregion polygons can be plotted using `geom_map()`, specifying that the map (i.e. the polygons) and the data (i.e. the colours filling the shapes) both come from the dataframe, `color = black` makes the shape outlines black:

```r
map_FEOW <- ggplot() +
	coord_map() +
	geom_map(data = shpData_FEOW_clipped_fort,
	 map = shpData_FEOW_clipped_fort,
	 aes(x = long, y = lat, map_id = id, group = group, fill = id),
	 color = "black", size = 0.5) +
	geom_point(colour = "red", alpha = 0.5, size = 0.5,
	 aes(x = decimallongitude, y = decimallatitude),
	 data = brown_trout) +
	theme_classic() +
	theme(legend.position="bottom") +
	theme(legend.title=element_blank()) + 
	xlab("Longitude") +
	ylab("Latitude")
```

<center><img src="{{ site.baseurl }}/img/map_feow.png" alt="Img" style="width: 700px;"/></center>


We can add extra elements using the `ggplot2` syntax, just like a normal `ggplot()`. Imagine that we want to indicate a potential area for a trout reintroduction program. Finland and Estonia have hardly any trout, but would probably have the right climatic conditions:

```r
map_FEOW_annot <- map_FEOW +
  annotate("rect", xmin = 20 , xmax = 35, ymin = 55, ymax = 65, fill="red", alpha=0.5) +
  annotate("text", x = 27.5, y = 61, size = 10, label = "Restock Area")
```

Finally, we can add a scale bar and a north arrow. To add these you can use the `ggsn` package.

Adding a scalebar. `dd2km` confirms whether the coordinates of the map are in decimal degrees, `dist` defines the distance for each gradation of the scalebar, `height` defines the height of the scalebar according to y axis measurements, so `0.01` is 0.01 decimal degrees latitude:

```r
map_FEOW_scale <- map_FEOW_annot +
	scalebar(location="topleft", data = shpData_FEOW_clipped_fort,
					 dd2km = TRUE, dist = 500, model='WGS84',
					 height = 0.01)
```

Adding a north arrow. Currently the default `north` command doesn't work properly, so we can't just do `map_FEOW + north()`. Instead `north2()` has to be used as a separate command. You can change the symbol by changing `symbol` to any integer from 1 to 8. You might get an error saying: "Error: Don't know how to add o to a plot" and your arrow might be placed in a strange location - you can change the values for `x` and `y` till your arrow moves to where you want it to be.

```r
north2(map_FEOW_scale, x = 0.2, y = 0.2, scale = 0.1, symbol = 1)
```

<center><img src="{{ site.baseurl }}/img/map_FEOW_annot.png" alt="Img" style="width: 700px;"/></center>

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
