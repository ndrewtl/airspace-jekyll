---
layout: post
title: Python Crash Course
subtitle: How to get started with Python
date: 2018-11-05T12:00:00.000Z
author: James
meta: python-crash-course
tags: intro_to_python
---

<div class="block">
  <center>
  <img src="{{ site.baseurl }}/img/tutheader-python_crash_course.png" alt="Img">
</center>
</div>

# Tutorial Aims:

#### 1. Learn how to install Python and start coding

#### 2. Learn the basics of Python

#### 3. Explore where you can go next on your Python journey

----
This tutorial is a whistle stop tour of Python, the aim is not to get you to be an expert by the end of it, but rather to lay the groundwork for you to start tackling your own Python challenges and to kick off your learning. After this tutorial I hope that you will understand the basics of python, know how and where you can write code, know where you can get more help when you are stuck and be enthused by the idea of learning more.

----
# Steps:

#### <a href="#why">1. Why learn Python</a>

#### <a href="#installing">2. How to install Python with Anaconda</a>

#### <a href="#spyder">3. Writing Python code in Spyder</a>

#### <a href="#variables">4. Python basics - variables and printing</a>

#### <a href="#operators">5. Python basics - simple maths and operators</a>

#### <a href="#functions">6. Python basics - functions</a>

#### <a href="#loops">7. Python basics - loops</a>

#### <a href="#ifs">8. Python basics - if-else statements</a>

#### <a href="finding_help_online">9. Finding help online</a>

#### <a href="#next_steps">10. Next steps</a>

----

<a name="why"></a>
## Why Python?

Python is one of the most used and most talked about programming languages that exist. It was designed to be easy to read and write from the moment it was designed. For this reason it is a great language to learn if you are new to coding. However python has many other benefits including
 - It is free and open source, you will never have to pay to use Python
 - It is widely used and has a large user base, therefore you will always be able to find help online
 - It is the most used language for machine learning and data science
 - It is multi-purpose and you can do anything from making pretty graphs, to training neural networks, to running simulations, to web scraping, web hosting, making games and much more
 - Python has many great and free libraries (add-ons) which you can use without having to write all your code from scratch
 - Python is a great tool for statistics, mathematics, data processing and modelling

Hopefully you are convinced that python is a great tool to add to your repertoire.

<a name="installing"></a>

## Installing Python with Anaconda

So now we want to know how to install Python and get straight into writing some knarly Python code to rule the world.

There is a distribution called Anaconda which is very popular with Python users and is a very powerful tool, we are going to install this. As I mentioned, Anaconda is a Python 'distribution', this basically means it is a Python bundle which comes with the Python language and some extras. When you install Anaconda you will also install Spyder (a application you can use to write Python code), and a few other things you don't need to worry about yet.

For this tutorial we will be working with Spyder within the Anaconda distribution, this will certainly be enough to get you started and get you far into the Python universe. Spyder is an IDE-integrated development environment (if you are an R buff then you can think of Spyder as RStudio for Python), it is basically the program you will use to write all of your code. If you are brand new to coding you can think about Spyder as being like Microsoft Word for writing Python code. In Microsoft Word you make a new document and write down your ideas in english (or any other wonderful language), if you make a typo then Microsoft Office will prompt you to fix your mistake. In Spyder you make a new 'script' and write down your ideas in Python, if you make a typo then Spyder will prompt you to fix it.

Here is a great video to show you how to install Anaconda if you have not got it already.

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/Vt6loGK9Adc?rel=0&amp;start=49&end=140" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe></center>

<br />Congratulations! You have just installed Python! Lets make sure that everything is working now.

Open up a Command Prompt (terminal) and type `conda --version`. If everything has been installed successfully then after a moments pause your conda version number should be printed to your screen.

<a name="spyder"></a>

## Writing Python in Spyder

Now we have Python installed it is time to launch Spyder. You can do this by launching the Anaconda Navigator from the start menu. When this starts up click on the Spyder application to open it up.

<center><img src="{{ site.baseurl }}/img/python_crash_course-spyder_demo.gif" alt="img" style="width: 900px;"/></center>

<br />Once you have launched Spyder you will see three main panels by default. You can edit the layout of these panels if you want but for this tutorial I will assume that you don't want to mess with that yet. On the left, the large panel is where you can write scripts. At the top of this panel you can see that there has been a script started for you called `temp.py`. If you wanted to you could write code into this script (similar to writing a MS Word document) and then save it to run later.

A script in python is basically the same as a script in literature. A script for a play is written by the author to tell the actors what they should do and say and in what order. A script for a python program is written by the author to tell the computer what it should do and it what order.

So when you write commands into the python script on the left, it is just like writing them in the regular script. You store your lines of dialogue (code) to be performed (run) later.

In the bottom right of the window you will see the console, and this is what we are going to focus on for this part of the tutorial. This is different to the script panel. **In the console**, whenever you **type a command and then press enter**, that command will be **run right away**, not stored for later like in the script. You can think of using the console as **similar to using a calculator**. Whenever you type something in it is run right away. You can see this in the demo below. First we tell the console what the variable `x` is; then we tell it to print `x` so that we can see it again. After this we tell it to print other products of `x`. Try typing these same lines of code into your own editor and see what happens.

<center><img src="{{ site.baseurl }}/img/python_crash_course-console_demo.gif" alt="img" style="width: 900px;"/></center>

<br />Note that whilst writing lines of code into the console I made a mistake and the console showed me an error message. In this case all I needed to do is fix the error and run the correct line.

<a name="variables"></a>

## Variables and Printing

In Python one of the basic things we can do is set variables. A variable is just a store, or a shortcut to refer to something else. In the example above I assigned the number 5 to the variable x, `x=5`. After I assigned the variable x (once I told the console that x was 5) then I could print out x and the console knew that it should print out the number 5. In Python we don't need to stick to letters for variables names, just like in your old algebra classes. If we want to we could tell the console that `x=5`, `my_variable=0`, and `yesterday=999`. After we have done this and we ask the console to `print(yesterday + x)` it should tell us that this is simply 1004. Why don't you try having a go at this?

**quick hints** - Python cares a lot about capitalisation and spaces.
- When you are naming a variable you cannot have any spaces in the variable name. So instead of using spaces, people often use underscores instead. This is why, in the example above, we used `my_variable` instead of `my variable`. Trying to assign a variable name with a space will cause an error.
- Python doesn't read the way we do, it is 'case sensitive'. This means as hard as it might try, it will never know that two variables like `strictly_come_dancing` and `Strictly_Come_Dancing` might be the same. You can use capitals in your variables but you just need to be consistent.

We can assign other things to variables as well. In Python the base types are integers, floating-point numbers, strings, booleans, lists and dictionaries.
Don't be put off! We will go through what each of these mean in turn and see why they might be useful, they are all very useful. Before we do that, I want to introduce you to two functions in Python. Namely the `print` and the `type` function.

#### The print function
We have seen this before when we printed x. The way to use this function is `print(the thing to be printed)`. You can print any valid piece of information in Python. Try printing some numbers.

#### The type function
You use this function to find out the type of any variable in Python. For example try entering the following into your console.
```python
x=5
print(type(x))
```
Based on what is printed here can you tell what type of variable x is? Try it again with `x=5.0` and see if you get a different answer.

#### Integers
Integers are just whole numbers, you probably learned to count them as a kid. We can set variables equal to integers by doing the following.
```python
x = 5
y=89
year=2018
```
Make up some variable names, like `x`, `y` or `ABBA` and give them integers values. Then print the type of these variables to make sure that they really are integers.

#### Floating-point numbers
Floating-point numbers are just numbers which have a point `.`, ie they are expressed as a decimal. _(Quick note that python was developed in american english and so decimals use a point instead of a comma eg $\frac{2}{5}=0.4$)_. Try making up some variable names give them floating point number (`float`) values. For example you might say `glass_fullness = 0.5`, or the more pessimistic of you might say `glass_emptyness = 0.5`. Then print the type of these variables to make sure that they are floats.

#### Strings
In Python strings are often used to store text variables. For example I might want to know that `coding_club_rating = 'Great'` or that `best_song = "Dancing Queen"`. Note that in python it does not matter whether we use single quotes `''` or double quotes `""` around some characters to make this into a string. **Anything which is between single or double quotes is a string**. Another more practical use might be to store the date as a string `date = '17-10-2018'` or to store the name of a species we are looking at `species = "killer whale"`. Try making up some variable names and give them string values. Afterwards print their types.

#### Lists
In Python anything which is surrounded by square brackets `[]` and comma spaced is a list. You can insert anything into a list including other lists, and the entries don't have to be the same type. We could make a list of numbers by assigning `these_numbers = [2, 78, 1, 0, 12]`, or dates by assigning `these_dates = ['12-08-1987', '02-05-1852', '25-12-1999']`, or of ages of trees by assigning `tree_ages = [1, 4.5, 1000, 19.7, 'older than time itself']`

Is it important that your lists have commas between each item, and that they start and end with square brackets.

##### Booleans
A Boolean variable is a variable that is either `True` or `False`. Having variables like this is useful in Python as it gives us a lot of flexibility. For example we might want to right some code which checks whether it is Friday and if so it tells us to go home early. In this code we could store the variable `is_it_friday = True` and then use this later.

#### Dictionaries
(*note dictionaries are a little harder to grasp than the rest of the material here, so feel free to skip this part and come back when you are ready*)
Dictionaries are a more specialised data type in Python. They are a little bit like a list, but each item in the list (each __value__) is given a name (a __key__). In a normal dictionaries you will find a list of definitions, where each definition has a __key__ (ie the word you look up).

For example if you look up _python_ (this would be the __key__) in the Oxford Engligh Dictionary you might find the __value__ :

"_a large heavy-bodied non-venomous snake occurring throughout the Old World tropics, killing prey by constriction and asphyxiation._"

In Python-dictionaries, your keys should be strings and your values can be any type. The values could be integers, floats, strings, lists, more dictionaries or anything else.

You will know something is a dictionary because __it will have curly brackets around it__. Here is an example of a dictionary used to store movie quotes
```python
my_dictionary = { "jurassic park": "life finds a way",
                  "terminator": ["i'll", "be", "back"]  }
```
The dictionary above has two keys, `'jurasic park'` and `'terminator'`. Dictionaries are always of the form `{key:value, key:value, key:value, ...}`. Between each key and its value we put a `:` and between each key:value pair we put a `:`. In `my_dictionary` the values are of different types. The value for the key 'jurassic park' is a string; whereas the value for the key 'terminator' is a list of strings.

We can access values in a dictionary by looking them up with their key. In the above example we could print the Jurassic Park quote by using `print(my_dictionary['jurassic park'])`. We could print the other quote by putting the other key into the square brackets of the print statement. In general you access the items in a dictionary by putting the name of the key into square brackets after your dictionary variable name. So if your dictionary is called `DrDictionary` and you want the value associated with the key 'coolKey' you would use `DrDictionary['coolKey']`.

- Now make your own dictionary of your own favourite movie quotes. Try storing the movie quotes as strings, lists, integers or floats and then print them.

####  

<a name="operators"></a>
# Simple Maths and Operators
All of the basic mathematical operators that you know and love, such as `+` and `-` are available in Python. In this section we are going to show and demo some of these operators.
###### <a href="#operators_add">- Addition and subtraction (numbers and strings)</a>
###### <a href="#operators_basic">- Other basic operators</a>
###### <a href="#operators_compare">- Comparison operators</a>
###### <a href="#operators_boolean">- Boolean operators (True/False logic)</a>

<a name="operators_add"></a>
###### Addition and subtraction (numbers and strings)

Python can be used essentially as a big calculator which can do all the calculations that you don't want to. It can multiply, divide, add, subtract etc etc.

The first thing you need to know is that the basic operators such as `+` and `-` act slightly differently depending on the data types you are using them on. For example adding two integers will give you what you expect, typing `56 + 19` into the console would give `75`; but adding two strings will 'concatenate' them (stick them together) `'Hello' + 'World'` would give `'HelloWorld'`.

Try adding some integers together and printing the result; then try the same with some strings and some floats.
<br />
eg:
- what is `'winter' + 'coming'`?
- what is `34 + 99`?
- what is `5.14 + 17.87`?
- what is `True + True`?

DEBUGGING QUESTION: what is `4 + 2` and what is `'4' + '2'` and why are the answers different?


Next you should try subtracting some integers and floats from each other and printing the results. Do you think you can subtract strings from each other?

<a name="operators_basic"></a>
###### Other basic operators

Now you have the gist of how operators work why not have some fun by playing with these shiny new ones
- `/` : divide : eg `20/4` (answer : 5)
- `*` : multiply : eg `14*3` (answer : 42)
- `%` : modulo: eg `12 % 5` (answer : 2)
- `**` : raise to power : eg `2**4` (answer : 16)

Try using each of these operators on integers, floats and strings. Not all of them will work on each data type and you will get some errors, but it is okay! To quote the famous mantra of silicon valley companies **'move fast, break things'** (not a good motto if you are an antiques dealer but great for learning Python)

<a name="operators_compare"></a>
###### Comparison operators

In Python we can also do comparisons between variables, between numbers or between strings. With these operators you can check when a number is greater than another number (to check your data set for mistakes, like is age greater than zero `age > 0`) or when a string is equal to another string (to filter your data set, like to a certain species name `species_name=='lama glama'`). This can be done using the comparison operators
- `>`: greater than : eg `5 > 10` (answer : False)
- `<`: less than : eg `-1 < 0`  (answer : True)
- `>=`: greater than or equal to : eg `17 >= 17` (answer : True)
- `<=`: less than or equal to : eg `9 <= 20` (answer : False)
- `==` : equal to : eg `1==0` (answer : False), `'lama glama'=='lama glama'` (answer : True)

Try doing some comparisons to make sure you understand how each of these work. Here is a list of things to try to get you started, but you don't have to stop there

<a name="operators_boolean"></a>
###### Boolean operators (True/False logic)

There is also a set of boolean operators in Python. They allow us to do operations on boolean variables. This can be perform certain logical tasks based on outcomes of other calculations.

Take these lines of code for example, where we get the user to type in their name and then comment on it
- `&` : logical and : `True & True` (answer : True), `True & False` (answer : False)
- `|` : logical or : `True | False` (answer : True), `False | False` (answer : False)
- `!` : logical not : `! True` (answer : False), `! False` (answer : True)

Can you guess, or get python to calculate, what `True | True` will be? How about `False & False`?



Note: One of the really nice things about Python is how much it can read like plain English by using **Python Keywords**. In the above examples you could replace, `&` with `and`, replace `|` with `or`, and replace `!` with `not` and still get the same answers. Why not try rewriting the exampes above using the `and`, `or` and `not` keywords instead of the symbols. I'll start you off

<center><img src="{{ site.baseurl }}/img/python_crash_course-boolean_logic.gif" alt="img" style="width: 700px;"/></center>

<br />
Using what you know so far can you solve Hamlet's dilemma below? What will the answer be if `to_be = True` or with `to_be = False
`
```python
to_be = True
print(to_be or not to_be)
```
<a name="loops"></a>
# Loops
In loops we write instructions that will be repeated a number of times in a row. We can use loops to repeat actions more efficiently.
<center>
<img src="{{ site.baseurl }}/img/python_crash_course-y_bird.gif" alt="img" style="width: 400px;"/>
<br />https://giphy.com/gifs/simpsons-dippy-bird-drinking-l41lUJ1YoZB1lHVPG
</center>

<br />Lets say you have more important work to do than pressing 'y', lets say for example that we would like to find the mean of some data.
```python
precip = [2,7,1,9,0,2,4,5]
```
If you were to do this manually with pen and paper you might decide to add them up in sequence. So you would take the first two numbers and add them (2+7=9) then add the next number to the current total (9+1=10), then add the next number in the list and so on until you have added all the numbers. At the end you would divide your sum by how many numbers you had (in this case 8). This is exactly the kind of situation we could use a loop for! Below is the python code to add up this list of numbers.
```python
# this is the list of number we would like to find the mean of
precip = [2,7,1,9,0,2,4,5]

# we make a variable total which we can add the items from the list to
total=0

# in this next line we say we will repeat this adding loop 8 times
# during this loop the variable i will take on the values 0-7, increasing by 1 on each pass
for i in range(8):
    # on each pass we add the next number to the total we have so far
    total = total + precip[i]

# finally we will divide by the number of items to get the mean
mean_precip = total / 8
```

Loops can be hard when you are new to coding and so it might take you a bit longer to really get your head round them.
- Try writing a loop to do the job of the drinking-bird above. Your loop should print the string `'y'` 10 times.
- Try writing a loop to add a list of 3 stings together. For example, if adding up the list `["hot", "line", "bling"]` your loop should create the variable `total = "hot line bling"`.

<a name="functions"></a>
# Functions
Functions are mini computing boxes that we write in Python. Functions take an input (we could call this x), do some computing with it, and output the result.
<center>
<img src="{{ site.baseurl }}/img/python_crash_course-function_diagram.png" alt="img" style="width: 300px;"/><br />
image credit <br /> https://hackernoon.com/a-simple-introduction-to-one-way-functions-a2429d427546
</center>

<br />We have been using two functions already, the `print` function and the `type` function. The `print` function takes an input (we have used integers, floats and strings!) and copies its input to the console.

Functions in Python are great because they allow us to repeat things easily. Lets say you have some data you want to process, such as daily precipitation rates for a few different sites. We would like to know the mean of each of these samples.

```python
daily_precipitation_edinburgh = [2,7,1,9,0,2,4,5]
daily_precipitation_glasgow = = [5,5,3,6,7,3,2,8]
daily_precipitation_dundee = = [4,2,5,7,2,6,8,7]
```

We could do this the way we did in the example above, copying and pasting our code 3 times, (or we could even make a loop within a loop) but this is untidy and as budding Pythonistas we can do better. Instead we can make a function which will calculate the mean of whatever we put in.

Note that in python we make a function by **defining** it (we use the Python `def` keyword). Below we write a function which calculates the mean of a list of 8 numbers.

```python
# the def keyword tells python you are about to make a function
# the variable name that comes after 'def' is the function name
# in this case our function is called my_mean
# x is a stand in for our input. We call it x but it could have been any variable name at all
def my_mean(x):
  # we make a variable total which we can add the items from the list to
  total=0

  # in this next line we say we will repeat this adding loop 8 times
  # during this loop the variable i will take on the values 0-7, increasing by 1 on each pass
  for i in range(8):
      # on each pass we add the next number to the total we have so far
      total = total + x[i]

  # finally we will divide by the number of items to get the mean
  mean_value = total / 8

  # in this final line we return the answer
  # the rest of the variables here, like total, will be thrown away
  return mean_value
```
Now that we have defined this function we can use it in the same way that we use the `print` function. We feed in an input and the function will do its job and return u the mean. To calculate the mean precipitation in Edinburgh we would use
```python
mean_precipitation_edinburgh = my_mean(daily_precipitation_edinburgh)
```
and we would get the answer 3.75

- Try using this function to find the mean precipitation in Glasgow and Dundee

Now that we have this function we could can use it again and again without having to rewrite the loop to calculate the mean, but only for lists of length 8.
- This function will only work properly for lists which are 8 items long. Try modifying this function to calculate the mean of any list that is input. *Hint: you can find the length of a list x by using* `len(x)`



<a name="ifs"></a>
# if-else statements
If else statements are used in Python so that one script can be used to do different things based on some variable. We might want a script which motivates us to work hard and play hard. So that if today is a Friday it tells us to go home early but for the rest of the week days it encourages us to work hard.

```python
# set the today variable
today='Thursday'

# check if today is friday
if today=='Friday':
  # if today is friday then this is printed
  print("Why not go home early?")
else:
  #if today is not friday then this is printed
  print("Hard work is a virtue! You can do it! I believe in you!")
```

<a name="imports"></a>
# Imports (packages)
The final thing you should know at the beginning of you Python journey is about packages (add-ons). *You will hear people talk about 'packages', 'modules' and 'libraries' in Python but they pretty much refer to the same thing*. Packages are other pieces of code that we can use in Python once we import them. When you installed anaconda you also installed over 100 packages that we have not used yet! This may seem daunting, but don't worry, you won't need to learn them all, and the idea of packages can seem confusing at first.

Imagine packages to be your friends with a range of different skills. When you need something done you can invite your friend over to do the work for you (they are selfless like that). Let me quickly introduce you to 3 friends who you should meet.

- **numpy** - numpy is great at doing things with numbers. Like sums, means, variances, matrix algebra, multiplication etc. If you need to do some sums, numpy is the one to call.
- **scipy** - scipy is really good at maths and stats. Invite them over for linear regression, numeric integration and tea etc.
- **matplotlib** - matplotlib is your artsy friend and likes to help you draw pretty graphs

You can invite a friend over by `import`ing them. When you invite them over you can also give them a shorter (or even longer) nickname if you don't like their real name. In the following snippet we will invite numpy over and get them to calculate a mean and standard deviation for us. We will give numpy the nickname 'np' because that is what everyone else calls them, but we could equally give them the name will, vivian, g or python_package_for_numbers.

```python
# first we invite numpy over : import numpy
# at the same time we give numpy the nickname np : as np
import numpy as np

# here is the data we want to investigate
x = [1,3,6,2,8,4,1]

# now that numpy (np) is here we can ask them to use their mean function
x_mean = np.mean(x)
# then we ask numpy to use its standard deviation function on the data
x_standard_dev = np.std(x)

# finally we will print the result
print(x_mean)
print(x_standard_dev)
```

The numpy, scipy and matplotlib packages are very popular friends and I don't have time to show you all their talents in this tutorial but if you google them you could easily find out more about their many skills.

*Note: Another friend you might want to meet is pandas. If you would like to load data from excel sheets and manipulate it, then pandas is the person to invite.*

<a name="finding_help_online"></a>
# Finding help online
One of the best things about Python is the Python community. There are millions of people using Python and so there are lots and lots of people trying to do similar things. This means that for almost any question you might have in python, like <a href="https://stackoverflow.com/questions/3090175/python-find-the-greatest-number-in-a-list-of-numbers">'how to I find the maximum value in a list of numbers'</a> or
<a href="https://stackoverflow.com/questions/25805239/get-nth-element-of-a-list">'how to I find the nth item in a list'</a> there are good online discussions out there. For most Python users this is THE way to work. Why spend lots of time struggling to write code when the answer to your problem is just a google search away?


##### Recipe for searching for code snippets

1. figure out what you are trying to do and boil it down to a short sentence
2. go to google and type *your sentence + 'python'*
3. Go through a few links (stackoverflow is the main website you'll want) and read about the problems other people are trying to solve
4. Copy and paste any good solutions you find
5. Modify the code if needed
6. Be nice and upvote helpful solutions

Lets go through an example. I have some data and I want to sort the values in the list in descending order. In the example below I would like the first item to be the 10, then the 9 then the 8 etc.

```python
my_data = [1,4,8,1,9,3,0,2,6,2,1,10]
```
I could write a loop to do this for me and it would be good practice for my Python skills, buit this time I am in a hurry and I'd rather not reinvent the wheel. So I'll google it instead.

<br />
<center>
<img src="{{ site.baseurl }}/img/python_crash_course-list_sort.gif" alt="img" style="width: 900px;"/>
</center>

<br />The link to the answer I found is <a href="https://stackoverflow.com/questions/25374190/how-to-sort-integer-list-in-python-descending-order">here</a>.
<br />As you can see I googled the question and had to go through two links to find a question that matched mine. I also had to redefine my question along the way to make it more specific to what I wanted. When I found a solution on stackoverflow I copied it and edited it before pasting it into my console.


Searching for answers to your coding problems is a major part of writing code effectively. This is something that you should get used to. By searching online can you find ways to accomplish the following:
 - add the number 50 to the end of the list `my_data` without just typing it in manually
 - convert the string `'15'` to an integer

<a name="next_steps"></a>
# Learning more basic Python
There are so many resources to learn Python out there, more than one person could hope to have even looked at. Therefore ! cannot give you a definitive best method to keep learning Python. However, here are some resources that I have come across that I have enjoyed.

##### Online interactive courses
I think these are a really good way to get started both with Python if you are new to it, but also with Python packages that you have never explored before. The benefit of these are that they give you a lot of structure to your learning and they make sure you are getting a hang of the basics before you move on.

These courses have material for you to read and/or watch and also interactive computing exercises. In the interactive exercises you fill in the blacks of some coding scripts and receive instant feedback on what you have written. There are a number of these out there but the two that I am personally acquainted with are

- <a href="https://www.codecademy.com/learn/learn-python">codeacademy</a> - free articles and coding exercises. Paid for quizes and other extras
- <a href="https://www.datacamp.com/tracks/skill">datacamp</a> - videos, articles and coding exercises. The first sections of each module are free but the more advanced stuff is paid

##### Blogs
Such as <a href="https://ourcodingclub.github.io">ourcodingclub</a>! These are great resources to follow, especially if you find blogs of people who are working in the same field as you. They can introduce you to Python tools specific to your domain. If you know some Python already then these are good resources to take you from intermediate to advanced.

##### Books
I have mixed views on books when it comes to coding. It is my own personal belief that the only way to learn how to code is to actually sit down and do it. However, a book can be a good synthesis of knowledge and they do have their place. One classic book is Numeric Recipes in Python but there are too many to mention here and new ones are coming out all the time.

##### Challenges
There are some websites which are specifically devoted to hosting challenges for people to complete or to compete in. If you are the type of person who likes a good challenge to enhance your learning then these might be for you.

- <a href="https://www.kaggle.com/">kaggle</a> - This is a platform which hosts machine learning competitions for learning, for kudos and even for prizes. If you are interested in diving in deeper into machine learning and data science then this is a nice hub.
- <a href="https://projecteuler.net/">project euler</a>- This is a site which hosts a catalogue of coding challenges for you to complete. It is a really nice way to find challenges where you can apply what you have learned. There are different difficulties as well so you should be able to find a challenge no matter where you are on your Python path.

<hr>
<hr>

__Check out <a href="https://ourcodingclub.github.io/workshop/" target="_blank">this page</a> to learn how you can get involved! We are very happy to have people use our tutorials and adapt them to their needs. We are also very keen to expand the content on the website, so feel free to get in touch if you'd like to write a tutorial!__

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/). <a href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://licensebuttons.net/l/by-sa/4.0/80x15.png" alt="Img" style="width: 100px;"/></a>

<h3><a href="https://www.surveymonkey.co.uk/r/F5PDDHV" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>
<br />
<h3>&nbsp; You can contact us with any questions on <a href="mailto:ourcodingclub@gmail.com?Subject=Tutorial%20question" target = "_top">ourcodingclub@gmail.com</a></h3>
<br />
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
<br />
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
