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

<a name="cube"></a>

**Learning outcome**: by the end of this section, you will be able to explain the capabilities and functionality of Iris cubes and coordinates.

The top level object in Iris is called a cube. A cube contains data and metadata about a single phenomenon and is an implementation of the data model interpreted from the *Climate and Forecast (CF) Metadata Conventions*.

Each cube has:

##### - A data array (typically a NumPy array).
##### - A "name", preferably a CF "standard name" to describe the phenomenon that the cube represents.
##### - A collection of coordinates to describe each of the dimensions of the data array. These coordinates are split into two types:
##### - Dimensioned coordinates are numeric, monotonic and represent a single dimension of the data array. There may be only one dimensioned coordinate per data dimension.
##### - Auxilliary coordinates can be of any type, including discrete values such as strings, and may represent more than one data dimension.

A fuller explanation is available in the <a href="http://scitools.org.uk/iris/docs/latest/userguide/iris_cubes.html">Iris User Guide</a>.


