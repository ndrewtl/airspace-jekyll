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

This short tutorial is based around exploring the Geosceince's weather station data located on top of the James Clark Maxwell Building at the University. You can have a look at all the data via the [link to the station webpage](https://www.ed.ac.uk/geosciences/weather-station/weather-station-data), but for ease of use, I've provided the data file that we'll be using here. The file is in the commonly used csv format. We are going to look at some of the data from [Storm Eleanor](https://www.metoffice.gov.uk/barometer/uk-storm-centre/storm-eleanor), which passed over the UK and Edinburgh on the 2nd-3rd January.

JCMB_StormEleanor_2_3_Jan.csv

### Just the basics!

We are going to start off simple, using the basic 'core' Python language features to explore the data, then later in the tutorial we'll look at some of the ways we can use modules and libraries to make dealing with data easier.

```python
weatherfile = open("StormEleanor_2_3_Jan.csv", "r")

for line in weatherfile:
  print(line)

weatherfile.close()
```

It's good practice in Python to use a keyword called `with` when you are reading from (or writing to) data files. The `with` keyword ensures that files are automatically closed properly at the end of their use, and system resources are correctly freed up. You could think of it intuitively like, "**With** this file opened **as** this shorthand name, I am going to do these things in the following block of code..."

```python
with open("StormEleanor_2_3_Jan.csv", "r") as weatherfile:
  for line in weatherfile:
    print(line)
```

Note how when using `with` we do not have to worry about closing the file -- it is taken care of automatically when we exit the code block. `with` also makes sure that any exceptions that occur when opening the file are dealt with appropriately.

We can load the data in from the file and print it to screen, but that probably isn't much practical use. How should we approach reading the data into variables that we can manipulate and perform calculations on? We can do this by assigning the values in the file to the basic Python data structure, the **list**. (We shall discover later that lists are not necessarily the best data struture for numerical data, but they are a good introduction when learning Python.)

Firstly, our csv file is separated by commas, but we need to get rid of these before we can start doing useful things with the data. In fact, although it is obvious to us that we are dealing with numeric data, Python is just treating the text file as a bunch of lines of text, rather than numbers. In Python (and many other langauges), this type of data is refered to as a *string*. Try changing the `print(line)` function in the above code snippet to: `print(type(line))` and run the program again. You should get this output:


```python
<type 'str'>
```

`str` is short for *string*, i.e. text or characters. Oh no! W have just got one long string of text from our data, including all the commas from the csv file format. Luckily, Python is very good at manipulating strings. We can break up the data by *splitting* the string. Like so:

```python
with open("StormEleanor_2_3_Jan.csv", "r") as weatherfile:
  for line in weatherfile:
    print(line.split(','))
```

We should get output that looks like this:

```python
...
['1239882', '252.5', '3.466666', '4.3', '6.5', '78', '978.0999', '0\n']
...
```

We also probably want the data separated by the columns, so we can do calculations on each column of data, like wind-speed, rainfall, pressure, and so on.

Let's suppose we are interested in the `air pressure` from our data file. Air pressure is stored in the 7th column of the text file. However, Python, like many other programming langauges, starts counting from *zero*, so the columns of each line are numbered 0, 1, 2, 3, 4, 5, 6, 7. So to get the seventh column we actually use the number 6:

```python
with open("StormEleanor_2_3_Jan.csv", "r") as weatherfile:
  for line in weatherfile:
    data_row = line.split(',')
    pressure = data_row[6]
    print(pressure)
```

We've broken this down into stages now. First we create a variable called `data_row` to store each line of the text file as a **list** as we read it in. Then we get each value of pressure by *indexing* the `data_row` list with the number 6. Finally we print the `pressure` value to screen. Run the above code and you should get all the pressure values printed out. 

This is okay, but we are just printing out values of pressure, not storing them anywhere. In fact we are overwriting the value of `pressure` every time we go through the `for` loop. So we are going to create a list of pressure values that we can store and reuse. 

```python
pressure_data = []

with open("StormEleanor_2_3_Jan.csv", "r") as weatherfile:
  for line in weatherfile:
    data_row = line.split(',')
    pressure = data_row[6]
    pressure_data.append(pressure)
```

We now have a data structure called `pressure_data` that contains all the air pressure measurements from the text file. But there are a couple of problems here. (Can you think what they might be?)

Hint: Think about

 1. The very first line in the original text file
 2. The type of the data in the list...

Yes, unfortunately, we have two problems: 1. The first text line in the original file ("Pair_avg") has been read into the list, which is not good if we want to try and sum or average the list later, for example. 2. The items in the list are actually still strings, not numbers! You can test this by inserting the following line at the end of the code:

```python
# Oh no! This is the header line!
print(pressure_data[0])   # Prints: 'Pair_avg'

# Argh! This is a string!
print(type(pressure_data[1])  # Prints: 'str'
```

No worries, we can fix this with Python. To skip the header line, we can use a handy built-in function in Python called `next()`. `next()` can be used on objects or data structures in Python to simply mean "Go to the next item in this object". By adding `next(weatherfile)`, we are telling Python to take us to the next line before we start to do anything else.

Python is normally quite good at inferring what type of data you are dealing with, but sometimes it needs a hint. We can do this by converting our `pressure` variable from a string to a floating-point number by doing: `float(pressure)`

With the above amendments, your script should now look like:

```python
pressure_data = []

with open("StormEleanor_2_3_Jan.csv", "r") as weatherfile:
  for line in weatherfile:
    data_row = line.split(',')
    pressure = data_row[6]
    pressure_data.append(float(pressure))
```

Add print statements to check that the type of data is no longer strings, and that we have skipped over the header line containing the description text.

### Python's core language is simple, but limited

This all seems a bit long-winded, doesn't it? Isn't Python meant to be quick and easy, I hear you cry? 

Correct. Python's simple and hopefully intuitive syntax is nice, but the real strength of Python is in it's support for packages and libraries that make your coding life easier.  

Python actually has built in support for reading text and csv files, using a module (or library) called...`csv`! So there is no need to do all of the above every time you want to read in a simple text file. But I hope it was useful introduction to the feel of Python syntax, and some of the basic language features -- they will come in handy later!

To use the `csv` library in Python, we have to *import* it first, which is just a way of saying we want to bring this module into our Python program and use its features. 

```python
import csv

pressure_data = []   # Create an empty list

with open('StormEleanor_2_3_Jan.csv', 'rb') as csvfile:
  next(csvfile)
  for row in csv.reader(csvfile, quoting=csv.QUOTE_NONNUMERIC):
    pressure_data.append(row[6])

# Check our variables look okay and they are the correct type:
print(pressure_data)
print(type(pressure_data[1])
```

Using the built-in `csv` module is *okay*, it's a bit nicer than the manual version we made using only the core Python language but there are *much* better alternatives available by using one of the many available Python *packages*.

### Numeric Python: NumPy to the rescue!

*If you have not already done so, you will need to install the 'numpy' Python package*.

We are going to dive right in here and start using a Python package called NumPy. Packages are ubiquitous in Python, and most scientific programming done with Python makes use of one or more packages. You can think of them as 'add-ons' to the basic Python language, much like libraries in R or other programming languages. NumPy is short for *numerical Python* and contains a whole bunch of useful functions and data structures for dealing with primarily numerical data. 

We need to tell Python that we want to use the NumPy package (it is not available by default), so we use an `import` statement to do this, i.e. we want to *import* the package into our program so we can use its features. (Just like we did with the csv module)

(The only practical difference between `csv` and `numpy` is that `csv` is part of the standard Python library.)

```python
import numpy as np

data = np.loadtxt('StormEleanor_Jan_2_3.csv', delimiter=',')

```
That's it! Two lines of code :)

Let's break down the above to see what is happening. After we import numpy, we can now use function in numpy using the abbreviated form `np`. We then access the features of numpy by putting a dot `.` after `np`, and then typing the name of the function we want to use. The dotted notation is used a lot in Python: it's a shorthand way of grouping similar functions and data structures together, like saying, "Get me the `loadtxt` function from the `numpy` module.

In this case, we are using the `loadtxt` function to load a text based file (after all, a csv file is just a text file). We need to give the loadtxt function two arguments: the path and name of the file ("JCMB_Jan_2017.csv"), and the *delimiter* used in this type of text file. Since we are using a csv file (comma separated variable file), the delimiter is a comma. The delimiter must go inside quotation marks. 

Finally, note that we have assigned the result of the loadtxt function call to a variable we have created called `data`.




