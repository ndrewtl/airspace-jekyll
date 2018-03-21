---
layout: post
title: Introduction to Python
subtitle: Importing and exploring data with Python, writing good scientific code
date: 2019-01-26 00:00:00
author: Declan
meta: "PythonBasics"
tags: intro_to_python
---
<div class="block">
          <center><img src="{{ site.baseurl }}/img/tutheaderintro.jpg" alt="Img"></center>
        </div>

### Tutorial aims:

#### 0. Understand why Python is so useful for scientific programming

#### 1. Learn how to import tabular data

#### 2. Learn how to apply the same operations to multiple values

#### 3. Learn how to store many values together

#### 4. Learn how to perform the same operations of many different values

#### 5. Making programs do different things based on different values

#### 6. Learn about functions in Python

#### 7. Learn how to deal with errors in Python

#### 8. Making programs more reliable

#### 9. Learn how to debug scientific code

#### 10. Learn how to write Python programs for the command line


## Why Python for scientific programming?

You may have heard about the Python programming language before. It is often talked about as the next "Up and coming" programming language, or described as being a new, "trendy" programming language that everyone should be learning, particularly scientists. I am going to argue that Python is no longer merely "up and coming", or even particularly new, but one of the most popular and useful programming languages you could invest time in learning. In fact, as of 2018, Python is (by certain measures) **the most widely used programming language in the world**. So if you are a scientist, researcher, or student doing any kind of data analysis, or numeric programming, then I think Python is worth investing some time in learning, even just the basics.

Python is a programming language, a tool used to make computers do useful things for scientific coders much faster than they could do using conventional tools like spreadsheets or plotting software (and certainly much faster than manual calculations!). But programming languages are not really designed for computers at all. In fact, your computer has no idea what all the words and symbols in a piece of code written in Python actually *mean*. (It only understands ones and zeros and electrical currents.) [footnote]. The reason is that programming languages are actually designed for *humans* to have a convenent way of programming a computer without getting involved in things like binary and hexadecimal codes, and worrying about electronic circuitry inside the computer. 

## Why Python?

### 1. Readability

Python shines because it is designed to be *readable* for us humans. Python is often described as a language that is intuitive and relatively easy to learn. The **syntax** (how you arrange the set of words and symbols to make a Python program) is meant to be intuitve to humans by being similar to natural human languages in many ways. For example, look at these little snippets of Python and see if you can guess what they mean and what might happen if we told the computer to run the code:

```python
"Python".startswith("P")
```
This bit of python code reads like: *Python starts with a "P"*, and that is exactly what it means  in Python!. If we ran this bit of code, the computer would print out `True` on the screen.

What about this one?

```python
"thon" in "Python"
```
(Imagine reading it like a question...)

So if we ask: *"thon" in "Python"?*, the answer is yes (or True), because the letters "thon" appear in the word "Python". If we wrote:

```python
"xyz" in "Python"
```
we would get False, because those letters are not in the word "Python".

Python syntax has many more similarities with natural languages, and we will discover more throughout this tutorial. Hopefully this will make learning the Python language more intuitive (and fun, as we can compare it to human languages (well, English...)).

Here is one more bonus round. Can you guess what might happen if we ran this Python code?

```python
tastyword = "chocolate"
x = 3

if tastyword.count("o") < x and tastyword.endswith("e"):
  print("You have won some tasty chocolate!")
```
>
### 2. General Puropose

Python has a major advantage when compared to some other commonly used programming languages in the scientific community; it is a *general purpose* programming language. Compared to other languages such as Matlab, IDL, ncl, and R, which were designed with specific applications in mind, Python was built as a general purpose programming language (like Java, C, Ruby etc.). This means you can use Python to write your data analysis code, plot the results of the analysis, write a numerical model, run a website, do your tax return...the list goes on. 

Because of it's general-purpose design, Python is used in the real world in a range of industries. Python is used by scientists at universities across the world, developers at big tech companies like Amazon, Facebook, and Google, by financial services companies, and social media apps like Facebook and Instagram, for example. In short, while this tutorial focuses on scientific applications of Python, you are learning a programming language that has a huge variety both within and outwith the scientific community.

### 3. Scientific Python Community

The third reason I'm going to mention is the community behind Python. As mentioned before, writing code is as much a way of communicating between humans trying to solve the same scientific problems as it is telling the computer what to do. Python has a very friendly and active community supporting it, many of whom are found on internet resources such as forums and the popular StackOverflow Q&A site. 

If you are stuck with a problem in Python, online resources are so plentiful that is often enough to just type "How do I do _X_ in Python", into a search engine - the first few results often will contain your answer. (And often the top link is a StackOverflow question asked by someone with the same or very similar problem to you.

In the domain of science, the Scientific Python community is just as well established. You may have already heard of Python packages like Numpy (Numerical Python), SciPy (Scientific Python), as well as other tools like Pandas, matplotlib, and others. Many of these tools were developed by scientists to share something back to the Python community, and they have now grown and become almost _de facto_ standard tools within the scientific programming community. 

## Let's go! Reading data with Python

Key Points that will be covered:

  - "Import a library into a program using `import libraryname`."
  - "Use the `numpy` library to work with arrays in Python."
  - "Use `variable = value` to assign a value to a variable in order to record it in memory."
  - "Variables are created on demand whenever a value is assigned to them."
  - "Use `print(something)` to display the value of `something`."
  - "The expression `array.shape` gives the shape of an array."
  - "Use `array[x, y]` to select a single element from a 2D array."
  - "Array indices start at 0, not 1."
  - "Use `low:high` to specify a `slice` that includes the indices from `low` to `high-1`."
  - "All the indexing and slicing that works on arrays also works on strings."
  - "Use `# some kind of explanation` to add comments to programs."
  - "Use `numpy.mean(array)`, `numpy.max(array)`, and `numpy.min(array)` to calculate simple statistics."
  - "Use `numpy.mean(array, axis=0)` or `numpy.mean(array, axis=1)` to calculate statistics across the specified axis."
  - "Use the `pyplot` library from `matplotlib` for creating simple visualizations."

This short tutorial is based around exploring the Geosceince's weather station data located on top of the James Clark Maxwell Building at the University. You can have a look at all the data via the [link to the station webpage](https://www.ed.ac.uk/geosciences/weather-station/weather-station-data), but for ease of use, I've provided the data file that we'll be using here. The file is in the commonly used csv format.

JCMB_Jan_2017.csv

Python has built in support for reading csv files, using a module (or library) called...csv. To use the `csv` library in Python, we have to *import* it first, which is just a way of saying we want to bring this module into our Python program and use its features. 

```python
import csv

with open('JCMB_2017_Jan.csv', 'rb') as csvfile:
  rainfallreader = csv.reader(csvfile)
  for row in rainfallreader:
    print(row)
```

If we run the script, we should just see our csv file printed out to the terminal.

But we probably want to more than that with our data! Let's think about how we could extact the rainfall data. The variable `row` we create in the for loop is a Python `list` type, and we can get individual items from the row list by *indexing*. You may have come across indexing in other langauges. Indexing is a way of saying we want the n-th item in a list or other data sequence. 

Python starts counting from zero, so to get the first item in the row list, we would write:

```python
row[0]
```




Using `csv` is okay, but it's a bit 

We are going to dive right in here and start using a Python package called NumPy. Packages are ubiquitous in Python, and most scientific programming done with Python makes use of one or more packages. You can think of them as 'add-ons' to the basic Python language, much like libraries in R or other programming languages. NumPy is short for *numerical Python* and contains a whole bunch of useful functions and data structures for dealing with primarily numerical data. 

We need to tell Python that we want to use the NumPy package (it is not available by default), so we use an `import` statement to do this, i.e. we want to *import* the package into our program so we can use its features. (Just like we did with the csv module)

(The only practical difference between `csv` and `numpy` is that `csv` is part of the standard Python library.)

```python
import numpy as np

data = np.loadtxt('JCMB_Jan_2017.csv', delimiter=',')

```

Let's break down the above to see what is happening. After we import numpy, we can now use function in numpy using the abbreviated form `np`. We then access the features of numpy by putting a dot `.` after `np`, and then typing the name of the function we want to use. The dotted notation is used a lot in Python: it's a shorthand way of grouping similar functions and data structures together, like saying, "Get me the `loadtxt` function from the `numpy` module.

In this case, we are using the `loadtxt` function to load a text based file (after all, a csv file is just a text file). We need to give the loadtxt function two arguments: the path and name of the file ("JCMB_Jan_2017.csv"), and the *delimiter* used in this type of text file. Since we are using a csv file (comma separated variable file), the delimiter is a comma. The delimiter must go inside quotation marks. 

Finally, note that we have assigned the result of the loadtxt function call to a variable we have created called `data`.




