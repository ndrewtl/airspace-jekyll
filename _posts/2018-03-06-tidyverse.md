---
layout: post
title: Manipulation and visualisation of spatial and population data
subtitle: Cleaning occurrence data and customising graphs and maps
date: 2018-03-06 10:00:00
author: Gergana
meta: "Tutorials"
tags: data_manip data_vis github
---
<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheaderoccur.png" alt="Img">
	</center>
</div>

### Tutorial Aims:

#### <a href="#create"> 1. Create a coding tutorial and host it on GitHub </a>

#### <a href="#github"> 2. Set up version control with GitHub and RStudio </a>

#### <a href="#tidyverse"> 3. Analyse and visualise data using the tidyverse </a>

#### <a href="#markdown"> 4. Create a reproducible report using Markdown </a>


<p></p>

#### All the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-occurrence" target="_blank">this repository</a>. Click on `Clone/Download/Download ZIP` and unzip the folder, or clone the repository to your own GitHub account.

<a name="create"></a>
<center><img src="{{ site.baseurl }}/img/CodingClub_logo2.png" alt="Img" style="width: 700px;"/></center>


__We started Coding Club to help people at all career stages gain statistical and programming fluency, facilitating the collective advancement of ecology across institutions and borders. We use in-person workshops and online tutorials to equip participants not only with new skills, but also with the means to communicate these new skills broadly via online tutorials.__

__We would love to extend Coding Club beyond the University of Edinburgh and create a supportive community of people keen to get better at coding and statistics! With that in mind, we present you with a workshop on how to write and share tutorials!__


<center><img src="{{ site.baseurl }}/img/74b26610-2027-11e7-841b-f91777fdfcdf.png" alt="Img" style="width: 700px;"/></center>

There are similar initiatives already in place, including in Ghent University, University of Aberdeen and University of St Andrews, which is very exciting!

## How does a Coding Club workshop work?
There are many ways to run a coding workshop and different approaches might work better in different situations. Here is how we usually structure our workshops. The workshops take two hours and begin with a super short presentation or introductory talk about what we will be doing, what skills we will acquire and what they are useful for. We then direct workshop attendants to the link for the tutorial around which the workshop is focused. People usually open the tutorial on half of their screen and `RStudio` on the other half.

<center><img src="{{ site.baseurl }}/img/workshop.png" alt="Img" style="width: 650px;"/></center>

At each workshop, we have a team of demonstrators who are there to answer questions and help out. We find that it works well to let people go through the tutorial at their own pace and we usually walk around and check whether things are going fine. Most of the tutorials have challenges at the end, for which people can work individually or in small teams. We bring cookies, popcorn and other treats, occasionally make bad R jokes and try our best to make the atmosphere light and positive. We don't require people to sign up and there are no obligations to attend all the workshops: people are free to attend whichever workshops are of interest to them. At the end of the workshops, we usually stay behind for a while in case people have any specific questions about their own coding projects.

## 1. Create a coding tutorial and host it on GitHub

We write our tutorials in Markdown. Markdown is a language with plain text formatting syntax. Github and Markdown work very well together and we use Markdown because we can turn a Markdown file into a website hosted on Github in a minute or so! Because of the syntax formatting, Markdown is a great way to display code: the code appears in chunks and stands out from the rest of the text. All of the Coding Club tutorials are written in Markdown.

<center><img src="{{ site.baseurl }}/img/atom_rstudio.png" alt="Img" style="width: 1000px;"/></center>

We use the Atom text editor, which is a user-friendly text editor and easy on the eyes. You can use another text editor, like Brackets or TextEdit on a Mac and Notepad on a Windows computer if you prefer, the principle is the same. A plain text editor is a programme, which allow you to create, save and edit various types of text files, like `.txt` and in our case, Markdown (`.md`) files. So for example, `Microsoft Word` is a text editor, but not a plain one. In the "fancier" plain text editors, you get "syntax" highlighting: different types of text, like code and links, are colour coded so they are easier to spot.

__You can <a href="https://atom.io/" target="_blank">download Atom here</a>, if you wish, but it's a fairly large file, so you can also proceed with whatever text editor you already have and you can check out Atom later.

You can also open the tutorial template in RStudio, but note that there are small differences between Markdown and GitHub-flavoured Markdown (the curly brackets):__

```r
# Traditional Markdown
# ```{r}
# some code
# ```

# GitHub-flavoured Markdown
# ```r
# some code
# ```
```

Our workflow tends to go like this:

#### - Write the `R` code for the tutorial in `RStudio`

#### - Save any graphs you create with your code

#### - Open a text editor, copy and paste your `R` code in the tutorial template

#### - Save the file as a `.md` file

#### - Add text to explain the purpose of the tutorial and what the code does

#### - Add images and links as suitable


#### Don't worry if you've never used a text editor or `Markdown` before. We have created a template you can open straight in Atom (or another plain text editor) and just insert your text, code and images.

## You can download the  `tut_template.md` file that you can turn into a tutorial and the brief R script for the tutorial from this <a href="https://github.com/ourcodingclub/CC-EAB-tut-ideas" target ="_blank">GitHub repository.</a> Click on Clone/Download Zip, download the files and unzip them.

__Open the file `tut_template.md` in Atom. The file includes instructions on how to add subheadings, links, code and images.__

We are using `<a href="#section_number">text</a>` to create anchors within our text. For example, when you click on section one, the page will automatically go to where you have put `<a name="section_number"></a>`.

To create subheadings, you can use `#`, e.g. `# Subheading 1` creates a subheading with a large font size. The more hashtags you add, the smaller the text becomes. If you want to make text bold, you can surround it with `__text__`, which creates __text__. For italics, use only one understore around the text, e.g. `_text_`, _text_.

When you have a larger chunk of code, you can paste the whole code in the `Markdown` document and add three backticks on the line before the code chunks starts and on the line after the code chunks ends. After the three backticks that go before your code chunk starts, you can specify in which language the code is written, in our case `R`.

To find the backticks on your keyboard, look towards the top left corner on a Windows computer, perhaps just above `Tab` and before the number one key. On a Mac, look around the left `Shift` key. You can also just copy the backticks from below.

### Publish your tutorial on Github

__Next we can publish our tutorial on GitHub, which will turn it into a website, whose link you can share with your peers - transferring quantitative skills among ecologists in action!__

__Go to the GitHub website, register if you don't already have an account (it's free) and click on `New Repository`.__

<center> <img src="{{ site.baseurl }}/img/new_repo_eab.png" alt="Img" style="width: 600px;"/> </center>

Choose a name for your repository: that will form part of the link for your online tutorial so choose something short and informative. Add a brief description, click on `Initialize with a README.md` and then click on `Create repository`.

<center> <img src="{{ site.baseurl }}/img/new_repo_eab2.png" alt="Img" style="width: 600px;"/> </center>

#### Now you can see your new repository. Click on `Upload files` and upload your filled in `Markdown` template. Make sure you save the file as `index.md` - that will make your tutorial the landing (home) page of the website. Upload any images you are using in your tutorial as well.

You are two clicks away from having a website with your tutorial! Now click on `Settings` and scroll down to the `GitHub pages` section. We need to enable the `GitHub pages` feature, which turns our `index.md` file into a page, i.e. website. Change `Source` from `None` to `master` - the master branch of our repository. Click on `Save`.

<center> <img src="{{ site.baseurl }}/img/github_pages.png" alt="Img" style="width: 600px;"/> </center>

#### Congratulations, your repository is now published as a website!

__Scroll down to the `GitHub pages` section again - you can see the link for your tutorial! If you need to edit your tutorial, you can go back to your repository, select the `index.md` file, then click on `Edit` and make any necessary changes. You can also check out different themes for your website, though the default one is clean and tidy, which works well for coding and statistics tutorials in general.__

<a name="github"></a>

## 2. Set up version control with GitHub and RStudio

### What is version control?

Version control allows you to keep track of your work and helps you to easily explore what changes you have made, be it data, coding scripts, or manuscripts. You are probably already doing some type of version control, if you save multiple files, such as `Dissertation_script_25thFeb.R`, `Dissertation_script_26thFeb.R`, etc. This approach will leave you with tens, if not hundreds, of similar files, it makes it rather cumbersome to directly compare different versions, and is not easy to share among collaborators. What if by the time your supervisor/co-author has finished commenting on `Dissertation_script_26thFeb.R`, you are already on `Dissertation_script_27thFeb.R`? With version control software such as <a href="https://git-scm.com/" target = "blank">Git</a>, version control is much smoother and easier to implement. Using an online platform like <a href = "https://github.com/" target="blank">Github</a> to store your files also means that you have an online back up of your work, so you won't need to panic when your laptop dies or your files mysteriously disappear.

### How does GitHub work?

#### You make a repository (a folder that is under version control) and you have two copies of it - a local copy (on your computer) and a remote copy (online on GitHub). Repositories can be public or private - if you would like to have free private repositories, you can apply <a href="https://education.github.com/discount_requests/new">here</a> using your institutional email address.

## The GitHub workflow can be summaried by commit-pull-push.


### Commit
__Once you've saved your files, you need to commit them - this means they are ready to go up on GitHub (the online copy of the repository).__


### Pull
__Now you need to pull, i.e. make sure you are completely up to date with the online version of the files - other people could have been working on them even if you haven't.__


### Push
__Once you are up to date, you can push your changes - at this point in time your local copy and the online copy of the files will be the same.__

__Each file on GitHub has a history, so instead of having many files like `Dissertation_1st_May.R`, `Dissertation_2nd_May.R`, you can have only one and by exploring its history, you can see what it looked at different points in time.__

For example, here is the history for a script. Obviously it took me a while to calculate those model predictions!

<center> <img src="{{ site.baseurl }}/img/filehistory.png" alt="Img" style="width: 1200px;"/> </center>

You can embed this workflow within `RStudio` using projects and enabling version control for them - we will be doing that shortly in the tutorial. You can use git through the command line, or through RStudio and/or GitHub desktop.

### What are the benefits of using GitHub as a lab?

Having a GitHub repo for your lab makes it easy to keep track of collaborative and personal projects - all files necessary for certain analyses can be held together and people can add in their code, graphs, etc. as the projects develop. Each file on GitHub has a history, making it easy to explore the changes that occurred to it at different time points. You can review other people's code, add comments on certain lines or the overall document, and suggest changes. For collaborative projects, GitHub allows you to assign tasks to different users, making it clear who is responsible for which part of the analysis. You can also ask certain users to review your code. Overall, GitHub presents a great opportunity to have an online back up copy of your work, whilst also doing version control, and it can also make it easier to discuss code, as well as write and edit code collaboratively.

### Make a new GitHub repository and sync it with RStudio

#### What is a repository?
GitHub uses repositories - you can think of a repository (_aka_ a repo) as a "master folder" - a repository can have folders within it, or be just separate files. In any case, a repository is what holds all of the files associated with a certain project that is version-controlled.

To make a repository, go to `Repositories/New repository` - choose a concise and informative name that has no spaces or funky characters in it. This can be your master repo that holds together past and ongoing research, data, scripts, manuscripts. Later on you might want to have more repositories - e.g. a repository associated with a particular project that you want to make public or a project where you are actively seeking feedback from a wide audience.

<center> <img src="{{ site.baseurl }}/img/newrepo.png" alt="Img" style="width: 1200px;"/> </center>

Click on `Initialise repo with a README.md file`. It's common practice for each repository to have a `README.md` file, which contains information about the project/lab group, what is the purpose of the repository, as well as any comments on licensing and data sources. Github understands several text formats, among which `.txt` and `.md`. `.md` stands for a file written in <a href="https://en.wikipedia.org/wiki/Markdown">Markdown</a> - you might have used Markdown before from within `RStudio` to create reports of your code and its outputs. You can also use Markdown to write plain text files, for example the file you are reading now was written in Markdown.

<center> <img src="{{ site.baseurl }}/img/newrepo2.png" alt="Img" style="width: 1200px;"/> </center>

You can directly edit your `README.md` file on Github by clicking on the file and then selecting `Edit this file`.

<center> <img src="{{ site.baseurl }}/img/readme.png" alt="Img" style="width: 1200px;"/> </center>


#### Exercise 1: Write an informative README.md file
You can now write the `README.md` file for your repository. To make headings and subheadings, put hashtags before a line of text - the more hashtags, the smaller the heading will appear. You can make lists using `-` and numbers `1, 2, 3, etc.`.

#### Exercise 2: Writing a `.gitignore` file
In a file called `.gitignore`, you can specify which files you want git to ignore when users make changes and add files. Examples include temporary Word, Excel and Powerpoint files, `.Rproj` files, `.Rhist` files etc. You might also have gigantic files that are only stored on your local copy, e.g. if you are working in a group repository, other users might not need them and they'll take up unnecessary space on their computers.

Go to `Create new file` and write a `.gitignore` file within the main repository (i.e. not in a subfolder). You need to call the file `.gitignore` and then add the types of files that Git should ignore on separate lines. You can make this specific to your needs, but as a start, you can copy over this code:

```
# Prevent users to commit their own RProject
.Rproj.user
.Rproj
# Prevent users to commit their own .Rhistory in mutual area
.Rhistory
.Rapp.history
# Temporary files
*~
~$*.doc*
~$*.xls*
*.xlk
~$*.ppt*
# Prevent mac users to commit .DS_Store files
*.DS_Store
# Prevent users to commit the README files created by RStudio
*README.html
*README_cache/
#*README_files/
```

### GitHub etiquette

It's a good idea to define some rules on how to use a repository, particularly if it is shared among many users.

__Here is a set of sample GitHub rules:__

```
Keep your scripts in your personal scripts folder. Don't look in other people's folders.
When working on group projects, move the script out of your personal folder to the relevant project folder, so that everyone can work on it.
Keep file paths short and sensible.
Upload your data on GitHub and use relative file paths - if the data are on your computer, and you have e.g. `data <- read.csv("C:/user/Documents/bird_abundance.csv")` in your code, only you will be able to read in that data, since it's only on your computer. But if you load the data from the lab's repo, every member of the repo can use it, e.g. `data <- read.csv("data/bird_abundance.csv")`, where `data` is a folder within the lab's repo.
Don't use funky characters and spaces in your file names, these cause trouble because of differences in Mac/Windows systems.
Always pull before you push in case someone has done any work since the last time you pulled - you wouldn't want anyone's work to get lost or to have to resolve many coding conflicts.
```

### Sync your GitHub rep with RStudio
We are now ready to start using your repository - first you need to create a local (i.e. on your computer) copy of the repository and create an RStudio project for the repo.

__Click `Clone or download` and copy the HTTPS link (that's the one that automatically appears in the box).__

<center> <img src="{{ site.baseurl }}/img/clone.png" alt="Img" style="width: 1200px;"/> </center>

Now open `RStudio`, click `File/ New Project/ Version control/ Git` and paste the link you copied from Github. Select a directory on your computer - that is where the "local" copy of your repository will be (the online one being on Github).

On some Macs, RStudio will fail to find Git. To fix this, first make sure all your work is saved then close R Studio, open up a terminal window by going to `Applications/ Utilities/ Terminal` then install <a href = "https://brew.sh" target="_blank">Homebrew</a> by typing the following, then pressing Enter:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now enter:

```
brew install git
```

and follow any instructions in the terminal window, you may need to enter your Mac's password or agree to questions by typing `yes`. Now you should be able to go back to RStudio and repeat the steps above to clone the git repository. We can't guarantee the above fix for Mac will work forever, some googling may be required.

Once the files have finished copying across, you will notice that a few things about your `RStudio` session have changed:

<center><img src="{{ site.baseurl }}/img/project2.png" alt="Img" style="width: 1200px;"/></center>

__The working directory in the top left corner is set to your local copy of the lab's repository.__ You can load in data using `read.csv("data/your_file.csv")` - this would load a `.csv` file in a folder called `data` within your lab's repository - notice that there is no need to include the repository's name - by setting up a RStudio project, you are already within it. Similarly, when saving files, you can specify the folder where you want them saved without the repository's name.

__There is a `Git` tab in the top right panel of RStudio.__ We will be doing our version control using the options within this tab.

__All the files that were in the repository online are now on your computer as well.__

# Tell RStudio who you are on GitHub
In the top right corner of the RStudio screen, click on `More/Shell`.

<center> <img src="{{ site.baseurl }}/img/shell.png" alt="Img" style="width: 900px;"/> </center>

### Copy the following code:

```
git config --global user.email your_email@example.com
# Add the email with which you registered on GitHub and click Enter

git config --global user.name "Your GitHub Username"
# Add your username and click Enter
```

### If it worked fine, there will be no messages and you can close the shell window - you only need to do this once.

### Make a new script file and go through commit - pull - push
Click on `File/New file/R Script` and type a one line comment like `# This is a test file.`. Save the file - you will see its name appear under the Git tab in the top right corner of the `RStudio` window. Click on the file, then on `Commit`, write a quick message and commit. Then click on `Pull` first and `Push` afterwards - given that you just made this repo, you'll probably get a message saying you are all up to date when you pulled - this means that everything that is in the remote (online) copy is also on your local copy on your computer. After you've pushed, everything on your local copy will appear on the remote copy - if you go to your repository on GitHub, you'll see your test file.

### Potential problems

Sometimes you will see error messages as you try to commit-pull-push. Usually the error message identifies the problem and which file it's associated with, if the message is more obscure, googling it is a good step towards solving the problem.

#### Code conflicts
While you were working on a certain part of a script, someone else was working on it, too. When you go through commit-pull-push, GitHub will make you decide which version you want to keep. This is called a code conflict, and you can't proceed until you've resolved it. You will see arrows looking like `>>>>>>>>>` around the two versions of the code - delete the version of the code you don't want to keep, as well as the arrows, and save the file. Then open the git shell, type `git add path-to-your-file/your-file.R` where you should replace the filepath with the one leading to the problem file. Then hit `Enter` and close the shell window. Now you should be able to commit again without issues.

# Contribute to an existing repo & get set up for the `tidyverse` tutorial

#### Log into your Github account and navigate to <a href = "https://github.com/ourcodingclub/CC-7-Github" target="_blank">the repository for the `tidyverse` tutorial </a>. Click `Fork` - this means you are making a copy of this repository to your own Github account - think of it as a working copy.

<center><img src="{{ site.baseurl }}/img/fork.png" alt="Img" style="width: 1000px;"/></center>

This is a tiny repo, so forking it will only take a few seconds, note that when working with lots of data, it can take a while. Once the forking is done, you will be automatically redirected to your forked copy of the `CC-7-Github` repo. Notice that now the repo is located within your own Github account - e.g. where you see "gndaskalova", you should see your name.

<center><img src="{{ site.baseurl }}/img/fork2.png" alt="Img" style="width: 1000px;"/></center>

Click `Clone or download` and copy the HTTPS link.

Now open RStudio, click `File/ New Project/ Version control/ Git` and paste the HTTPS link into the `Repository URL:`. You can have more than one `RStudio` project and you can have multiple `RStudio` windows open with a project each - e.g. if you go to `File/Recent projects`, you should see the project you made earlier.

#### What is the difference between forking and cloning?
If you had just cloned the `tidyverse` repository (i.e. copying the HTTPS link of the original repository that is hosted on the Coding Club account), then the repository still remains associated with the Coding Club account -  then everyone reading this tutorial would have been working in the same repository. In this case, we thought it would be nice if everyone has their own space, i.e. one working copy per person, so that's why you fork the repo first, which gives you a copy hosted on your account, and that is the copy you clone to your computer.

#### You are now all set up for the `tidyverse` tutorial!

<a name="tidyverse"></a>
## 3. Analyse and visualise data using the tidyverse

### Learning Objectives

### PART 1: Intro to the tidyverse
#### How to analyse population change of forest vertebrates

1. How to write a custom ggplot2 function
2. How to use gather() and spread() from the tidyr package in the tidyverse
3. How to parse numbers using parse_number() from the readr package in the tidyverse
4. How to use the distinct() function from dplyr in the tidyverse
5. How to use the filter() function from dplyr in the tidyverse
6. How to use the mutate() function from dplyr in the tidyverse
7. How to use the summarise()/summarize() function from dplyr in the tidyverse
8. How to use the tidy() function from the broom package to summarise model results
9. How to use the select() function from dplyr in the tidyverse

# Model population change for vertebrate forest species and see whether
# greater population change is found for longer duration studies

```r
# Packages ----
library(tidyverse)  # Hadley Wickham's tidyverse - the theme of this tutorial
library(broom)  # To summarise model outputs
library(ggExtra)  # To make pretty graphs - addon package to ggplot2
library(maps)  # To make pretty maps - warning: maps masks map from purr!
library(RColorBrewer)  # To make pretty colours
library(gridExtra)  # To arrange multi-plot panels
```

```r
# Setting a custom ggplot2 function ---
# *** Functional Programming ***
# This function makes a pretty ggplot theme
# This function takes no arguments!
theme_LPD <- function(){
  theme_bw()+
    theme(axis.text.x = element_text(size = 12, vjust = 1, hjust = 1),
          axis.text.y = element_text(size = 12),
          axis.title.x = element_text(size = 14, face = "plain"),             
          axis.title.y = element_text(size = 14, face = "plain"),             
          panel.grid.major.x = element_blank(),                                          
          panel.grid.minor.x = element_blank(),
          panel.grid.minor.y = element_blank(),
          panel.grid.major.y = element_blank(),  
          plot.margin = unit(c(0.5, 0.5, 0.5, 0.5), units = , "cm"),
          plot.title = element_text(size = 20, vjust = 1, hjust = 0.5),
          legend.text = element_text(size = 12, face = "italic"),          
          legend.title = element_blank(),                              
          legend.position = c(0.5, 0.8))
}
```

```r
# Load data ----
load("scripts/users/gdaskalova/GHENT/LPDdata_Feb2016.RData")

# Inspect data ----
head(LPDdata_Feb2016)
```

```r
# Format data for analysis ----

# Transform from wide to long format usign gather (opposite is spread)
# *** gather() function from the reshape package in the tidyverse ***
LPD_long <- gather(data = LPDdata_Feb2016, key = "year", value = "pop", select = 26:70)
```

```r
# Get rid of the X in front of years
# *** parse_number() from the readr package in the tidyverse ***
LPD_long$year <- parse_number(LPD_long$year)

# Rename variable names for consistency
names(LPD_long)
names(LPD_long) <- tolower(names(LPD_long))
names(LPD_long)

# Create new column with genus and species together
LPD_long$species.name <- paste(LPD_long$genus, LPD_long$species, sep = " ")

# Get rid of strange characters like " / "
LPD_long$country.list <- gsub(",", "", LPD_long$country.list, fixed = TRUE)
LPD_long$biome <- gsub("/", "", LPD_long$biome, fixed = TRUE)

# Examine the tidy data frame
head(LPD_long)
```

```r
# Data manipulation ----

# *** piping from from dplyr
LPD_long2 <- LPD_long %>%
  # Remove duplicate rows
  # *** distinct() function from dplyr
  distinct(LPD_long) %>%
  # remove NAs in the population column
  # *** filter() function from dplyr
  filter(is.finite(pop)) %>%
  # Group rows so that each group is one population
  # *** group_by() function from dplyr
  group_by(id) %>%  
  # Make some calculations
  # *** mutate() function from dplyr
  mutate(maxyear = max(year), minyear = min(year),
         # Calculate duration
         duration = maxyear - minyear,
         # Scale population trend data
         scalepop = (pop - min(pop))/(max(pop) - min(pop))) %>%
  # Keep populations with >5 years worth of data and calculate length of monitoring
  filter(is.finite(scalepop),
         length(unique(year)) > 5) %>%
  # Remove any groupings you've greated in the pipe
  ungroup()
```

```r
# Calculate summary statistics for each biome
LPD_biome_sum <- LPD_long2 %>%
  # Group by biome
  group_by(biome) %>%
  # Create columns, number of populations
  #  *** summarise()/summarize() function from dplyr in the tidyverse ***
  summarise(populations = n(),   
            # Calculate the mean study length
            mean_study_length_years = mean(duration),
            # Model sampling method
            dominant_sampling_method = names(which.max(table(sampling.method))),
            # Model unit type
            dominant_units = names(which.max(table(units)))) %>%
  # Remove any groupings you've greated in the pipe
  ungroup()

# Take a look at some of the records
head(LPD_biome_sum)
```

```
# Subset to just temperate forest species -----
  # Notice the difference between | and & when filtering
  # | is an "or" whereas & is "and", i.e. both conditions have to be met
  # at the same time
LPD_long2$biome <- as.factor(LPD_long2$biome)
LPD.forest <- filter(LPD_long2, biome == "Temperate broadleaf and mixed forests" |
                                      biome == "Temperate coniferous forests")
```

```r
# Data visualisation ----
# Data distribution - a histogram
(forest.hist <- ggplot(LPD.forest, aes(x = scalepop)) +
   geom_histogram(aes(fill = biome),
                  position = "identity", colour = "grey40") +
   geom_vline(aes(xintercept = mean(scalepop)),  # Adding a line for mean abundance
              colour = "darkred", linetype = "dashed", size = 1) +
   scale_fill_manual(values = c("#66CD00", "#53868B")) +
   theme_LPD() +
   labs(title = "a) Data distribution\n") +
   guides(fill = F)) # Hiding the legend - this will be a two plot panel
# thus we don't need the same legend twice
```

```r
# Density histogram of duration of studies in the two biomes
(duration.forests <- ggplot(LPD.forest, aes(duration, colour = biome)) +
   stat_density(geom = "line", size = 2, position = "identity") +
   theme_LPD() +
   scale_colour_manual(values = c("#66CD00", "#53868B")) +
   labs(x = "\nYears", y = "Density\n", title = "b) Monitoring duration\n"))
```

```r
# Arrange in a panel and save
forest.panel <- grid.arrange(forest.hist, duration.forests, ncol = 2)
ggsave(forest.panel, file = "forest_panel.png", height = 5, width = 10)
```

```r
# Calculate population change for each forest population
# 1785 models in one go!
# Using a pipe
forest.slopes <- LPD.forest %>%
  # Group by the key variables that we want to interate over
  group_by(decimal.latitude, decimal.longitude, class, species.name, id, duration, location.of.population) %>%
  # Create a linear model for each group
  do(mod = lm(scalepop ~ year, data = .)) %>%
  # Extract model coefficients using tidy() from the
  # *** tidy() function from the broom package ***
  tidy(mod) %>%
  # Filter out slopes and remove intercept values
  filter(term == "year") %>%
  # Get rid of the column term as we don't need it any more
  #  *** select() function from dplyr in the tidyverse ***
  dplyr::select(-term) %>%
  # Remove any groupings you've greated in the pipe
  ungroup()
```r

```r
# Visualising model outputs ----

# Plotting slope estimates and standard errors for all populations and adding histograms along the margins
(all.slopes <- ggplot(forest.slopes, aes(x = duration, y = estimate)) +
         geom_pointrange(aes(ymin = estimate - std.error,
                             ymax = estimate + std.error),
                         alpha = 0.3, size = 0.3) +
         geom_hline(yintercept = 0, linetype = "dashed") +
         theme_LPD() +
         ylab("Population change\n") +
         xlab("\nDuration (years)"))

(density.slopes <- ggExtra::ggMarginal(
  p = all.slopes,
  type = 'density',
  margins = 'both',
  size = 5,
  col = 'gray40',
  fill = 'gray'
))

# Save the plot
ggsave(density.slopes, filename = "slopes_duration.png", height = 6, width = 6)
```

### PART 2: Using pipes to make figures with large datasets
How to print plots of population change for multiple taxa

10. How to set up file paths and folders in R
11. How to use a pipe to plot many plots by taxa
12. How to use the purrr package and functional programming

```r
# PART 2: Using pipes to make figures with large datasets ----

# First we will do this using dplyr and a pipe

# Make histograms of slope estimates for each taxa -----
# Set up new folder for figures
# Set path to relevant path on your computer/in your repository
path1 <- "Taxa_Forest_LPD/"
# Create new folder
dir.create(path1)
```

```r
forest.slopes %>%
# Select the relevant data
dplyr::select(id, class, species.name, estimate) %>%
# Group by taxa
group_by(class) %>%
# Save all plots in new folder
do(ggsave(ggplot(.,aes(x = estimate)) +
            # Add histograms
            geom_histogram(colour="darkgreen", fill="darkgreen", binwidth = 0.02) +
            # Use custom theme
            theme_LPD() +
            # Add axis lables
            xlab("Rate of population change (slopes)"),
            # Set up file names to print to
            filename = gsub("", "", paste0(path1, unique(as.character(.$class)),
                                          ".pdf")), device = "pdf"))
```

### Intro to the purrr package ----
Now let's use purrr instead of dplyr to do the same thing

```r
# First let's write a function to make the plots
# *** Functional Programming ***
# This function takes one argument x, the data vector that we want to make a histogram
plot.hist <- function(x) {
  ggplot() +
  geom_histogram(aes(x), colour="darkgreen", fill="darkgreen", binwidth = 0.02) +
  theme_LPD() +
  xlab("Rate of population change (slopes)")
}
```

```r
# Here we select the relevant data
# Let's get rid of the other levels of 'class'
forest.slopes$class <- as.character(forest.slopes$class)
# Selecting the relevant data and splitting it into a list
taxa.slopes <- forest.slopes %>%
  dplyr::select(id, class, estimate) %>%
  spread(class, estimate) %>%
  dplyr::select(-id)
```

But what is purrr?  It is a way to "map" or "apply" functions to data
Here we are mapping the taxa.slopes data to the mean fuction
 *** map() function in purrr from the tidyverse ***

```r
taxa.mean <- purrr::map(taxa.slopes, ~mean(., na.rm = TRUE))
# This plots the mean population change per taxa
taxa.mean
```

Now we can use purr to "map" our figure making function
The first input is your data that you want to iterate over
The second input is the function

```r
taxa.plots <- purrr::map(taxa.slopes, ~plot.hist(.))
# We need to make a new folder to put these figures in
path2 <- "scripts/users/gdaskalova/GHENT/Taxa_Forest_LPD_purrr/"
dir.create(path2)
```

First we learned about map when there is one dataset, but there are many purrr functions
walk2 takes two arguments and returns nothing
In this case we just want to print the graphs, so we don't need anything returned
The first argument is our file paths, the second is our data and ggsave is our function

```r
# *** walk2() function in purrr from the tidyverse ***
walk2(paste0(path2, names(taxa.slopes), ".pdf"), taxa.plots, ggsave)
```

### PART 3: Downloading and mapping data from large datasets
#### Map the distribution of a forest vertebrate species and the location of monitored populations

13. How to download species IUCN status
14. How to download GBIF records
15. How to map occurence data and populations
16. How to make a custom function for plotting figures

```r
### PART 3: Downloading and mapping data from large datasets ----
#### How to map distributions and monitoring locations for one or more taxa

# Packages ----
library(rgbif)  # To extract GBIF data
library(rredlist)  # To extract Red List information
library(CoordinateCleaner)  # To clean coordinates
library(gridExtra)  # To make pretty graphs
library(ggrepel)  # To add labels with rounded edges
library(png)  # To add icons
library(mapdata)  # To plot maps
library(ggthemes)  # To make maps extra pretty
```

```r
# Data formatting & manipulation ----

# Filter out population data for chosen species - red deer
deer.data <- LPD_long2 %>%
  filter(species.name == "Cervus elaphus") %>%
  dplyr::select(id, species.name, location.of.population, year, pop)

# Filter out population estimates for chosen species - red deer
deer.slopes <- forest.slopes %>%
  filter(species.name == "Cervus elaphus")
```

```r
# Download species occurrence records from the Global Biodiversity Information Facility
# *** rgbif package and the occ_search() function ***
# You can increase the limit to get more records - 5000 takes a couple of minutes
deer.locations <- occ_search(scientificName = "Cervus elaphus", limit = 5000,
                             hasCoordinate = TRUE, return = "data") %>%
# Simplify occurrence data frame
dplyr::select(key, name, decimalLongitude, decimalLatitude, year, individualCount, country)
```

```r
# Make a new map and include the locations of the populations part of the Living Planet Database
(deer.map.LPD <- ggplot(deer.locations, aes(x = decimalLongitude, y = decimalLatitude)) +
    # Add map data
    borders("world", colour = "gray80", fill = "gray80", size = 0.3) +
    # Use custom map theme
    theme_map() +
    # Add the points from the population change data
    geom_point(alpha = 0.3, size = 2, colour = "aquamarine3") +
    # Specify where the data come from when plotting from more than one data frame using data = ""
    geom_point(data = deer.slopes, aes(x = decimal.longitude, y = decimal.latitude),
               size = 2, colour = "darkgreen"))
```

```r
# Customising map to make it more beautiful ----

# Check site names
print(deer.slopes$location.of.population)

# Beautify site names
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
                                             "Northern Yellowstone National Park" = "Yellowstone National Park")
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
                                             "Mount Rainier National Park, USA" = "Mount Rainier National Park")
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
  "Bow Valley - eastern zone, Banff National Park, Alberta" = "Banff National Park, Alberta")
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
  "Bow Valley - western zone, Banff National Park, Alberta" = "Banff National Park, Alberta")
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
  "Bow Valley - central zone, Banff National Park, Alberta" = "Banff National Park, Alberta")
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
  "Study area within Bow Valley, Banff National Park, Alberta" = "Banff National Park, Alberta")
deer.slopes$location.of.population <- recode(deer.slopes$location.of.population,
  "Bow Valley watershed of Banff National Park, Alberta" = "Banff National Park, Alberta")
```

```r
# Load packages for adding images
packs <- c("png","grid")
lapply(packs, require, character.only = TRUE)

# Load red deer icon
icon <- readPNG("reddeer.png")
icon <- rasterGrob(icon, interpolate = TRUE)
```

```r
# Update map
# Note - this takes a while depending on your computer
# I might add a version with less occurrences
(deer.map.final <- ggplot(deer.locations, aes(x = decimalLongitude, y = decimalLatitude)) +
    # For more localized maps use "worldHires" instead of "world"
    borders("world", colour = "gray80", fill = "gray80", size = 0.3) +
    theme_map() +
    geom_point(alpha = 0.3, size = 2, colour = "aquamarine3") +
    # We are specifying the data frame for the labels - one site has three monitored populations
    # but we only want to label it once so we are subsetting using data = beluga.slopes[1:3,]
    # to get only the first three rows and all columns
    geom_label_repel(data = deer.slopes[c(2, 4, 5, 9),], aes(x = decimal.longitude, y = decimal.latitude,
                                                     label = location.of.population),
                     box.padding = 1, size = 5, nudge_x = 1,
                     # We are specifying the size of the labels and nudging the points so that they
                     # don't hide data points, along the x axis we are nudging by one
                     min.segment.length = 0, inherit.aes = FALSE) +
    # We can recreate the shape of a dropped pin by overlaying a circle and a triangle
    geom_point(data = deer.slopes, aes(x = decimal.longitude, y = decimal.latitude + 0.6),
               size = 4, colour = "darkgreen") +
    geom_point(data = deer.slopes, aes(x = decimal.longitude, y = decimal.latitude - 0.3),
               size = 3, fill = "darkgreen", colour = "darkgreen", shape = 25) +
    # Adding the icon
    annotation_custom(icon, xmin = -210, xmax = -100, ymin = -60 , ymax = -30) +
    # Adding a title
    labs(title = "a. Red Deer GBIF occurrences", size = 12))
```

Now let's add some additional plots to our figure

```r
# Visualise the number of occurrence records through time ----
# This plot is more impressive if you have downloaded more records
# as GBIF downloads the most recent records first
yearly.obs <- deer.locations %>% group_by(year) %>% tally() %>% ungroup() %>% filter(is.na(year) == FALSE)

(occurrences <- ggplot(yearly.obs, aes(x = year, y = n)) +
    geom_smooth(colour = "aquamarine3", method = 'loess', size = 1) +
    labs(x = NULL, y = "Number of occurrences\n",
         title = "b. GBIF occurrences\n", size = 12) +
    # Use our customised theme, saves many lines of code!
    theme_LPD() +
    # if you want to change things about your theme, you need to include the changes after adding the theme
    theme(plot.title = element_text(size=12), axis.title.y = element_text(size=10)))
```

```r
# Visualise population trends ----
# Visualising the population trends of four deer populations

# Let's practice functional programming here
# *** Functional Programming ***
# Let's make a function to make the population trend plots
# First we need to decide what values the function needs to take
# x - The population data
# y - the slope value
# z - the location of the monitoring
# This function needs to take three arguments

# Okay let's make the ggplot function
pop.graph <- function(x, y, z) {
  # Make a ggplot graph with the 'x'
  ggplot(x, aes(x = year, y = pop)) +
  # Shape 21 chooses a point with a black outline filled with aquamarine
  geom_point(shape = 21, fill = "aquamarine3", size = 2) +
  # Adds a linear model fit, alpha controls the transparency of the confidence intervals
  geom_smooth(method = "lm", colour = "aquamarine3", fill = "aquamarine3", alpha = 0.4) +
  # Add the monitoring location 'y' into the plot
  labs(x = "", y = "Individuals\n", title = paste("c. ", y, "\n"), size = 7) +
  # Set the y limit to the maximum population for each 'x'
  ylim(0, max(x$pop)) +
  # Set the x limit to the range of years of data
  xlim(1970, 2010) +
  # Add the slope 'y' into the plot
  annotate("text", x = 1972, y = 0,  hjust = 0, vjust = -2, label = paste("Slope =", z), size = 3) +
  theme_LPD() +
  theme(plot.title = element_text(size=12), axis.title.y = element_text(size=10))
}
```

```r
# Find all unique ids for red deer populations
unique(deer.slopes$id)

# Create an object each of the unique populations
# Deer population 1 - Northern Yellowstone National Park
deer1 <- filter(deer.data, id == "6395")
slope_deer1 <- round(deer.slopes$estimate[deer.slopes$id == "6395"],2)
location_deer1 <- deer.slopes$location.of.population[deer.slopes$id == "6395"]
yellowstone <- pop.graph(deer1, location_deer1, slope_deer1)

# Deer population 2 - Mount Rainier National Park, USA
deer2 <- filter(deer.data, id == "3425")
slope_deer2 <- round(deer.slopes$estimate[deer.slopes$id == "3425"],2)
location_deer2 <- deer.slopes$location.of.population[deer.slopes$id == "3425"]
rainier <- pop.graph(deer2, location_deer2, slope_deer2)

# Deer population 3 - Switzerland
deer3 <- filter(deer.data, id == "11170")
slope_deer3 <- round(deer.slopes$estimate[deer.slopes$id == "11170"],2)
location_deer3 <- deer.slopes$location.of.population[deer.slopes$id == "11170"]
switzerland <- pop.graph(deer3, location_deer3, slope_deer3)

# Deer population 4 - Banff National Park, Alberta (there are more populations here)
deer4 <- filter(deer.data, id == "4383")
slope_deer4 <- round(deer.slopes$estimate[deer.slopes$id == "4383"],2)
location_deer4 <- deer.slopes$location.of.population[deer.slopes$id == "4383"]
banff <- pop.graph(deer4, location_deer4, slope_deer4)
```

```r
# Create panel of all graphs
# Makes a panel of the map and occurrence plot and specifies the ratio
# i.e., we want the map to be wider than the other plots
# suppressWarnings() suppresses warnings in the ggplot call here
row1 <- suppressWarnings(grid.arrange(deer.map.final, occurrences, ncol = 2, widths = c(1.96, 1.04)))
# Makes a panel of the four population plots
row2 <- grid.arrange(yellowstone, rainier, switzerland, banff, ncol = 4, widths = c(1, 1, 1, 1))

# Makes a panel of all the population plots and sets the ratio
# Stich all of your plots together
deer.panel <- grid.arrange(row1, row2, nrow = 2, heights = c(1.2, 0.8))

ggsave(deer.panel, filename = "deer_panel2.png", height = 10, width = 15)
```

If that wasn't challenging enough for you, we have a challenge for you to figure out on your own.
Take what you have learned about pipes and make a map for the five most well-sampled populations in the LPD database (the ones with the most replicate populations).
You get extra points for incorporating a handwritten function to make the map and for using purr to implement that function.

<a name="markdown"></a>

## 4. Create a reproducible report using Markdown

### What is R Markdown?

R Markdown allows you to create documents that serve as a neat record of your analysis. In the world of reproducible research, we want other researchers to easily understand what we did in our analysis. You might choose to create an R markdown document as an appendix to a paper or project assignment that you are doing, upload it to an online repository such as Github, or simply to keep as a personal record so you can quickly look back at your code and see what you did. R Markdown presents your code alongside its output (graphs, tables, etc.) with conventional text to explain it, a bit like a notebook. Your report can also be what you base your future methods and results sections in your manuscripts, thesis chapters, etc.

R Markdown uses <a href="http://www.markdowntutorial.com" target="_blank">markdown syntax</a>. Markdown is a very simple 'markup' language which provides methods for creating documents with headers, images, links etc. from plain text files, while keeping the original plain text file easy to read. You can convert Markdown documents to other file types like `.html` or `.pdf`.

## Download R Markdown
To get R Markdown working in RStudio, the first thing you need is the `rmarkdown` package, which you can get from <a href="https://cran.r-project.org/web/packages/rmarkdown/index.html" target="_blank">CRAN</a> by running the following commands in R or RStudio:

``` r
install.packages("rmarkdown")
library(rmarkdown)
```

## The different parts of an R Markdown file

### The YAML Header

At the top of any R Markdown script is a `YAML` header section enclosed by `` --- ``. By default this includes a title, author, date and the file type you want to output to. Many other options are available for different functions and formatting, see <a href="http://rmarkdown.rstudio.com/html_document_format.html" target="_blank">here for `.html` options</a> and <a href="http://rmarkdown.rstudio.com/pdf_document_format.html" target="_blank">here for `.pdf` options</a>. Rules in the header section will alter the whole document.

Add your own details at the top of your`.Rmd` script, e.g.:

```
---
title: "The tidyverse in action - population change in forests"
author: Gergana Daskalova
date: 22/Oct/2016
output: html_document
---
```

By default, the `title`, `author`, `date` and `output` format are printed at the top of your `.html` document.

Now that we have our first piece of content, we can test the `.Rmd` file by compiling it to `.html`. To compile your `.Rmd` file into a `.html` document, you should press the `Knit` button in the taskbar:

<img src="{{ site.baseurl }}/img/Knit_HTML_Screenshot.jpg" alt="Img">

 Not only does a preview appear in the `Viewer` window in RStudio, but it also saves a `.html` file to the same folder where you saved your `.Rmd` file.

<a name="insert"></a>

### Code Chunks

__Have a read through the text below to learn a bit more about how Markdown works and then you can start compiling the rest of your `.Md` file.__

#### The setup chunk

__This code chunk appears in `.Md` files in R by default, it won't appear in your html or pdf document, it just sets up the document.__

````
```{r setup, include = FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
````

#### The rest of the code chunks

This is where you can add your own code, accompanying explanation and any outputs. Code that is included in your `.Rmd` document should be enclosed by three backwards apostrophes ```` ``` ```` (grave accents!). These are known as code chunks and look like this (no need to copy this, just an example):

````
```{r}
norm <- rnorm(100, mean = 0, sd = 1)
```
````

Inside the curly brackets is a space where you can assign rules for that code chunk. The code chunk above says that the code is R code.

It's important to remember when you are creating an R Markdown file that if you want to run code that refers to an object, for example:

````
```{r}
plot(dataframe)
```
````

you must include the code that defines what `dataframe` is, just like in a normal R script. For example:

````
```{r}
A <- c("a", "a", "b", "b")
B <- c(5, 10, 15, 20)
dataframe <- data.frame(A, B)
plot(dataframe)
```
````

Or if you are loading a dataframe from a `.csv` file, you must include the code in the `.Rmd`:

````
```{r}
dataframe <- read.csv("~/Desktop/Code/dataframe.csv")
```
````

Similarly, if you are using any packages in your analysis, you have to load them in the `.Rmd` file using `library()` like in a normal R script.

````
```{r}
library(dplyr)
```
````

#### Hiding code chunks

If you don't want the code of a particular code chunk to appear in the final document, but still want to show the output (e.g. a plot), then you can include `echo = FALSE` in the code chunk instructions.


````
```{r, echo = FALSE}
A <- c("a", "a", "b", "b")
B <- c(5, 10, 15, 20)
dataframe <- data.frame(A, B)
plot(dataframe)
```
````

Sometimes, you might want to create an object, but not include both the code and its output in the final `.html` file. To do this you can use, `include = FALSE`. Be aware though, when making reproducible research it's often not a good idea to completely hide some part of your analysis:

__REMEMBER: R Markdown doesn't pay attention to anything you have loaded in other R scripts, you have to load all objects and packages in the R Markdown script.__

__Now you can start copying across the code from your tidyverse script and insert it into a code chunk in your `.Rmd` document. Better not to do it all at once, you can start with the first parts of the tidyverse script and gradually add on more after you've seen what the `.Rmd` output looks like.__

You can run an individual chunk of code at any time by placing your cursor inside the code chunk and selecting `Run -> Run Current Chunk`:

<img src="{{ site.baseurl }}/img/run_sel.png" alt="Img">

### Summary of  code chunk instructions

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l"><b>Rule</b></th>
    <th class="tg-yw4l"><b>Example</b><br>(default)</th>
    <th class="tg-yw4l"><b>Function</b></th>
  </tr>
  <tr>
    <td class="tg-yw4l">eval</td>
    <td class="tg-yw4l">eval=TRUE</td>
    <td class="tg-yw4l">Is the code run and the results included in the output?</td>
  </tr>
    <tr>
    <td class="tg-yw4l">include</td>
    <td class="tg-yw4l">include=TRUE</td>
    <td class="tg-yw4l">Are the code and the results included in the output?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">echo</td>
    <td class="tg-yw4l">echo=TRUE</td>
    <td class="tg-yw4l">Is the code displayed alongside the results?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">warning</td>
    <td class="tg-yw4l">warning=TRUE</td>
    <td class="tg-yw4l">Are warning messages displayed?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">error</td>
    <td class="tg-yw4l">error=FALSE</td>
    <td class="tg-yw4l">Are error messages displayed?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">message</td>
    <td class="tg-yw4l">message=TRUE</td>
    <td class="tg-yw4l">Are messages displayed?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">tidy</td>
    <td class="tg-yw4l">tidy=FALSE</td>
    <td class="tg-yw4l">Is the code reformatted to make it look “tidy”?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">results</td>
    <td class="tg-yw4l">results="markup"</td>
    <td class="tg-yw4l"><b> How are results treated? </b> <br> "hide" = no results <br>"asis" = results without formatting <br>"hold" = results only compiled at end of chunk (use if many commands act on one object)</td>
  </tr>
  <tr>
    <td class="tg-yw4l">cache</td>
    <td class="tg-yw4l">cache=FALSE</td>
    <td class="tg-yw4l">Are the results cached for future renders?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">comment</td>
    <td class="tg-yw4l">comment="##"</td>
    <td class="tg-yw4l">What character are comments prefaced with?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">fig.width, fig.height</td>
    <td class="tg-yw4l">fig.width=7</td>
    <td class="tg-yw4l">What width/height (in inches) are the plots?</td>
  </tr>
  <tr>
    <td class="tg-yw4l">fig.align</td>
    <td class="tg-yw4l">fig.align="left"</td>
    <td class="tg-yw4l">"left" "right" "center"</td>
  </tr>
</table>

## Inserting Figures
Inserting a graph into R Markdown is easy, the difficult bit is adjusting the formatting.

By default, RMarkdown will place graphs by maximising their height, while keeping them within the margins of the page and maintaining aspect ratio. If you have a particularly tall figure, this can mean a really huge graph. To manually set the figure dimensions, you can insert an instruction into the curly braces:

````
```{r, fig.width=2.5, fig.height=7.5}
ggplot(df, aes(x = x, y = y) + geom_point()
```
````

By default, figures are rendered as `.png` files by R Markdown, which can lead to loss of quality if your document is rescaled. You can change that to `.svg`, a vector file format by adding `dev='svg'` to the code chunk instruction section.

````
```{r, fig.width=2.5, fig.height=7.5, dev='svg'}
ggplot(df, aes(x = x, y = y) + geom_point()
```
````

## Inserting Tables

While R Markdown can print the contents of a data frame easily by enclosing the name of the data frame in a code chunk:

````
```{r}
dataframe
```
````

this can look a bit messy, especially with data frames with a lot of columns. Including a formal table requires more effort.

The most aesthetically pleasing and simple table formatting function I have found is `kable()` in the `knitr` package. The first argument tells kable to make a table out of the object `dataframe` and that numbers should have two significant figures. Remember to load the `knitr` package in your `.Rmd` file as well.

````
```{r}
kable(dataframe, digits = 2)
```
````

If you want a bit more control over the content of your table you can use ``pander()`` in the `pander` package. Imagine I want the 3rd column to appear in italics:

````
```{r}
emphasize.italics.cols(3)  # Make the 3rd column italics
pander(richness_abund)  # Create the table
```
````

Find more info on pander <a href="https://cran.r-project.org/web/packages/pander/pander.pdf" target="_blank">here</a>.

To learn more about the power of pipes check out:
http://dplyr.tidyverse.org/
http://r4ds.had.co.nz/pipes.html

To learn more about purr check out the following:
http://purrr.tidyverse.org/reference/map2.html
http://r4ds.had.co.nz/iteration.html

For more information on functional programming see:
http://r4ds.had.co.nz/functions.html

### Git in the command line
Traditionally, Git uses the command line to perform actions on local Git repositories. In this tutorial we ignored the command line but it is necessary if you want more control over Git. There are several excellent introductory guides on version control using Git, e.g. <a href = "http://simon-m-mudd.github.io/NMDM_book/#_version_control_with_git" target="_blank">Prof Simon Mudd's Numeracy, Modelling and Data management guide</a>, <a href = "https://swcarpentry.github.io/git-novice/" target="_blank">The Software Carpentry guide</a>, and this <a href = "https://github.com/BES2016Workshop/version-control" target="_blank">guide from the British Ecological Society Version Control workshop </a>. We have also created a neat cheatsheet with some basic Git commands and how they fit into the git/github ecosystem. A couple of the commands require [`hub`](https://github.com/github/hub) a wrapper for Git that increases its functionality, but not having this won't prevent you using the other commands:

<center><img src="{{ site.baseurl }}/img/git_cli.png" alt="Img" style="width: 1000px;"/></center>

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-baqh{text-align:center;vertical-align:top}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-baqh"><b>Command</b></th>
    <th class="tg-baqh"><b>Is <code>hub</code> required?</b></th>
    <th class="tg-baqh"><b>Origin</b></th>
    <th class="tg-baqh"><b>Destination</b></th>
    <th class="tg-baqh"><b>Description</b></th>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git fork</code></td>
    <td class="tg-baqh">Y</td>
    <td class="tg-yw4l">Other Github</td>
    <td class="tg-yw4l">Personal Github</td>
    <td class="tg-yw4l">Creates github repo in your personal account from a previously cloned github repo.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git clone git@github.com:user/repo.git</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">Personal Github</td>
    <td class="tg-yw4l">Local</td>
    <td class="tg-yw4l">Creates a local copy of a github repo called "repo" owned by the user "user". This can be copied from github.com.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git add README.md</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">Working Dir</td>
    <td class="tg-yw4l">Staging Area</td>
    <td class="tg-yw4l">Add "README.md" to staging area.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git commit -m "Message"</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">Staging Area</td>
    <td class="tg-yw4l">Local</td>
    <td class="tg-yw4l">Commits changes to files to the local repo with the commit message "Message".</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git commit -a -m "Message"</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">Working Dir</td>
    <td class="tg-yw4l">Local</td>
    <td class="tg-yw4l">adds and commits all file changes to the local repo with the commit message "Message".</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git pull</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">Personal Github</td>
    <td class="tg-yw4l">Local</td>
    <td class="tg-yw4l">Retrieve any changes from a github repo.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git push</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">Local</td>
    <td class="tg-yw4l">Personal Github</td>
    <td class="tg-yw4l">Sends commited file changes to github repo.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git create</code></td>
    <td class="tg-baqh">Y</td>
    <td class="tg-yw4l">Local</td>
    <td class="tg-yw4l">Personal Github</td>
    <td class="tg-yw4l">Create a github repo with the same name as the local repo.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git merge</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">NA</td>
    <td class="tg-yw4l">NA</td>
    <td class="tg-yw4l">Merge any changes in the named branch with the current branch.</td>
  </tr>
  <tr>
    <td class="tg-yw4l"><code>git checkout -b patch1</code></td>
    <td class="tg-baqh">N</td>
    <td class="tg-yw4l">NA</td>
    <td class="tg-yw4l">NA</td>
    <td class="tg-yw4l">Create a branch called "patch1" from the current branch and switch to it.</td>
  </tr>
</table>

<hr>
<hr>

<h3><a href="https://www.surveymonkey.com/r/C6BRZLH" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>

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
