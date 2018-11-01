---
layout: post
title: Analysing Earth science and climate data with iris
subtitle: Manipulate multi-dimensional climate data from common file formats
date: 2018-10-31 00:00:00
author: Declan Valters
meta: "PythonIris"
tags: python iris
---
<div class="block">
  <center><img src="{{ site.baseurl }}/img/tutheaderiris.png" alt="Img"></center>
</div>

_Material for this tutorial was adapted from the <a href="https://scitools.org.uk">SciTools</a> tutorial (SciTools is the group that maintain the Iris software.) It was adapted and modified under the GNU public licence v 3.0 for this OurCodingClub tutorial and we acknowledge appreciate the use of original source materials from SciTools - Thank you!_

Welcome to this tutorial in the Python series about the Iris python package. Iris is a powerful tool used for manipulating multi-dimensional earth science data. Iris is really useful when you are dealing with data from sources such as weather and climate models, particularly when it is stored in common formats such as NetCDF (a common data file format used in the climate science community.) 

Iris has data manipulation and visualisation features such as:

##### - A visualisation interface based on matplotlib and cartopy
##### - Unit conversion
##### - Subsetting and extraction of data
##### - Merge and concatenate
##### - Aggregations and reductions (including min, max, mean and weighted averages)
##### - Interpolation and regridding (including nearest-neighbor, linear and area-weighted)

If you need any of the above features and you find that you are **regularly writing your own custom functions in Python to do these things**, you may find that Iris already has these features availabe, and it can save you a lot of time in your work.

### Tutorial aims:

#### <a href="#understanding">1. Understand what Iris is</a>

#### <a href="#cube">2. Learn about the core Iris data structure: the Iris cube</a>


<a name="understanding"></a>

## What is Iris?

Iris was developed originally by the Met Office (UK) out of a need for dealing with the many file formats used in the weather, climate, and ocean sciences scientific community. Many users of Iris had previously had to write their own code from scratch to handle and manipulate these file-formats, such as NetCDF, GRIB, and other common (and not-so-common) formats, alternatively they had to use one of the many separately available packages for each type of file format. (Such as `python-netcdf4` for python, etc.). This resulted in a lot of duplicated effort from researchers re-writing what was effectively the same or very similar code. In addition, many operations on weather and climate data are essentially very similar, such as converting between different units, extracting subsets of the data, merging datasets, interpolating data, and so on. Iris was developed to bring together these operations and provide a file-format agnostic package to deal with these commonly used operations. 

Iris operates around a central data structure used to store multi-dimiensional data when you are working on it called a `cube`. This typically represents gridded data that has many levels as well as x and y dimensions (Though Iris is still useful for 2 dimesnional data as well.)

The third dimension in an Iris could be model levels, different heights in the atmosphere, or depths in the ocean. It could also be used to represent different time-slices in a model run. In short, the Iris cube data structure is very flexible and can be used to represent a large variety of different datasets.

We are going to have a look at how the Iris `cube` data structure works now, but first, let's test that we have iris installed:

```python
import iris
import numpy as np

print(iris.__version__)
print(np.__version__)
```

This should print out the version numbers of `iris` and `numpy`, the two main requirements for this tutorial.

If you do not have these two packages installed, see this guide on <a href="https://scitools.org.uk/iris/docs/latest/installing.html">installing iris</a>. (We assume you already have Python installed in your computing environmnet. 


<a name="cube"></a>

**Learning outcome**: by the end of this section, you will be able to explain the capabilities and functionality of Iris cubes and coordinates.

The top level object in Iris is called a cube. A cube contains data and metadata about a single phenomenon and is an implementation of the data model interpreted from the *Climate and Forecast (CF) Metadata Conventions*.

Each cube has:

##### - A data array (typically a NumPy array).
##### - A "name", preferably a CF "standard name" to describe the phenomenon that the cube represents.
##### - A collection of coordinates to describe each of the dimensions of the data array. These coordinates are split into two types:
###### - Dimensioned coordinates are numeric, monotonic and represent a single dimension of the data array. There may be only one dimensioned coordinate per data dimension.
###### - Auxilliary coordinates can be of any type, including discrete values such as strings, and may represent more than one data dimension.

A fuller explanation is available in the <a href="http://scitools.org.uk/iris/docs/latest/userguide/iris_cubes.html">Iris User Guide</a>.


Let's take a simple example to demonstrate the cube concept.

Suppose we have a ``(3, 2, 4)`` NumPy array:

<center> <img src="{{ site.baseurl }}/img/multi_array.png" alt="Img" style="width: 800px;"/> </center>

Where dimensions 0, 1, and 2 have lengths 3, 2 and 4 respectively.

The Iris cube to represent this data may consist of:

##### - a standard name of "air_temperature" and units of "kelvin"

##### - a data array of shape ``(3, 2, 4)``

##### - a coordinate, mapping to dimension 0, consisting of:
###### - a standard name of "height" and units of "meters"
###### - an array of length 3 representing the 3 height points
     
##### - a coordinate, mapping to dimension 1, consisting of:
###### - a standard name of "latitude" and units of "degrees"
###### - an array of length 2 representing the 2 latitude points
###### - a coordinate system such that the latitude points could be fully located on the globe
     
##### - a coordinate, mapping to dimension 2, consisting of:
###### - a standard name of "longitude" and units of "degrees"
###### - an array of length 4 representing the 4 longitude points
###### - a coordinate system such that the longitude points could be fully located on the globe
