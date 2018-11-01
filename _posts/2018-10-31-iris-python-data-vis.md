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

## The Iris Cube

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

Pictorially the cube has taken on more information than a simple array:

<center> <img src="{{ site.baseurl }}/img/multi_array_to_cube.png" alt="Img" style="width: 800px;"/> </center>

### Working with a cube

Whilst it is possible to construct a cube by hand, a far more common approach to getting hold of a cube is to use the Iris load function to access data that already exists in a file.

```python
fname = iris.sample_data_path('uk_hires.pp')
cubes = iris.load(fname)
print(cubes)
```

We can see that we've loaded two cubes, one representing the "surface_altitude" and the other representing "air_potential_temperature". We can infer even more detail from this printout; for example, what are the dimensions and shape of the "air_potential_temperature" cube?

Above we've printed the ``iris.cube.CubeList`` instance representing all of the cubes found in the given filename. However, we can see more detail by printing individual cubes:

```python
fname = iris.sample_data_path('uk_hires.pp')
cubes = iris.load(fname)

air_pot_temp = cubes[0]
print(air_pot_temp)
```

#### Cube attributes

We can create a single cube from the `load_cube` command. Iris also provides some sample data that we can work with in the `iris.sample_data_path` function. Printing a cube object in Python will give you an overview of the data it contains and the layout of that data:

```python
cube = iris.load_cube(iris.sample_data_path('A1B_north_america.nc'))
print(cube)
```
Which should print:
```
air_temperature / (K)               (time: 240; latitude: 37; longitude: 49)
     Dimension coordinates:
          time                           x              -              -
          latitude                       -              x              -
          longitude                      -              -              x
     Auxiliary coordinates:
          forecast_period                x              -              -
     Scalar coordinates:
          forecast_reference_time: 1859-09-01 06:00:00
          height: 1.5 m
     Attributes:
          Conventions: CF-1.5
          Model scenario: A1B
          STASH: m01s03i236
          source: Data from Met Office Unified Model 6.05
     Cell methods:
          mean: time (6 hour)
```

To access a cube's data array the ``data`` property exists. This is either a NumPy array or in some cases a NumPy masked array. It is very important to note that for most of the supported filetypes in Iris, the cube's data isn't actually loaded until you request it via this property (either directly or indirectly). After you've accessed the data once, it is stored on the cube and thus won't be loaded from disk again.

To find the shape of a cube's data it is possible to call ``cube.data.shape`` or ``cube.data.ndim``, but this will trigger any unloaded data to be loaded. Therefore ``shape`` and ``ndim`` are properties available directly on the cube that do not unnecessarily load data.

```python
cube = iris.load_cube(iris.sample_data_path('A1B_north_america.nc'))
print(cube.shape)
print(cube.ndim)
print(type(cube.data))
```

Which should display:
```
(240, 37, 49)
3
<class 'numpy.ma.core.MaskedArray'>
```


The ``standard_name``, ``long_name`` and to an extent ``var_name`` are all attributes to describe the phenomenon that the cube represents. The ``name()`` method is a convenience that looks at the name attributes in the order they are listed above, returning the first non-empty string. To rename a cube, it is possible to set the attributes manually, but it is generally easier to use the ``rename()`` method.

*From now on, we are not going to re-type the `cube = iris.load_cube(...)` line, it is assumed you will just change or append the lines below to your existing Python code. This is done to avoid having to reload the data into memory in each example!*

```python
print(cube.standard_name)
print(cube.long_name)
print(cube.var_name)
print(cube.name())

```

Check that you get the output:

```
air_temperature
None
air_temperature
air_temperature
```

There are a set of conventions used in climate data files called the "CF-conventions". These are standard names and units that are used to make interchanging and sharing data more consistent and straightforward. More about the CF-conventions can be read here: XXXX

Iris can deal with CF-convention formatted data, but it also supports non-CF named data too. To illustrate this, we can change the name of our cube (in other words, rename our dataset) and see how Iris deals with this:

```python
cube.rename("A name that isn't a valid CF standard name")
print(cube.standard_name)
print(cube.long_name)
print(cube.var_name)
print(cube.name())
```

Should print:

```
None
A name that isn't a valid CF standard name
None
A name that isn't a valid CF standard name
```

The ``units`` attribute on a cube tells us the units of the numbers held in the data array. We can manually change the units, or better, we can convert the cube to another unit using the ``convert_units`` method, which will automatically update the data array.

```python
print(cube.units)
print(cube.data.max())
cube.convert_units('Celsius')
print(cube.units)
print(cube.data.max())
```

Should give you:

```
K
306.0733
Celsius
32.9233
```

A cube has a dictionary for extra general purpose attributes, which can be accessed with the ``cube.attributes`` attribute:


```python
print(cube.attributes)
print(cube.attributes['STASH'])
```

Prints:

```
{'Conventions': 'CF-1.5', 'STASH': STASH(model=1, section=3, item=236), 'Model scenario': 'A1B', 'source': 'Data from Met Office Unified Model 6.05'}
m01s03i236
```

### Coordinates

As we've seen, cubes need coordinate information to help us describe the underlying phenomenon. Typically a cube's coordinates are accessed with the ``coords`` or ``coord`` methods. The latter *must* return exactly one coordinate for the given parameter filters, where the former returns a list of matching coordinates, possibly of length 0.

For example, to access the time coordinate, and print the first 4 times:









