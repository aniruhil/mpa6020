# Introduction to R and RStudio
PBIO 3150/5150 (Spring 2016)  
December 12, 2015  


# Installing R and RStudio
You can download R from [here](http://cran.us.r-project.org/) and RStudio from [here](http://www.rstudio.com/ide/download/). Be sure to download the appropriate version of each based on your computer's operating system. Once you have installed both R and RStudio, __launch RStudio__; if it finds R and you see something like the following application window (the one below is for the Mac OS X), you are good to go.   

<img src="Lab_1_files/figure-html/unnamed-chunk-1-1.png" title="" alt="" style="display: block; margin: auto;" />

Carefully observe the various panels and the tabs within each panel. Let us walk through some of these tabs as well as other features of RStudio.

# Basic Operations in RStudio
The console window shows you the R prompt $>$ where commands are initiated. You also see two panes to the right -- one called the __Environment__ where your data and any object you create will show up, and the other with several tabs __(History/Files/Plots/...)__.  

Use __File -> New File -> R Markdown__ to initiate a new R Markdown file. You will see a dialogue box (see below) where you can enter a title for the document, set the author's name, and choose between various formats (html, pdf, Word). You will use __Word__ as the default for all assignments and exams. 

<img src="Lab_1_files/figure-html/unnamed-chunk-2-1.png" title="" alt="" style="display: block; margin: auto;" />

Once you enter this information, give this file a name. The R Markdown file has several options (figure size, table of contents, etc.) that can be set by clicking on the gear icon in the pane's menu. The way R Markdown works is by allowing you to write text as you would in any word processor. If you want to start a new paragraph, hit __enter__ once on your keyboard to create a blank line. If you want to create a section heading start the section title with __#__ and subs-sections can be created with __##__. 

R Markdown allows you to embed any R commands you wish to run within a block of code that starts and ends with three back-ticks (```) as shown below.

<img src="Lab_1_files/figure-html/unnamed-chunk-3-1.png" title="" alt="" style="display: block; margin: auto;" />

There are several options one can use to control what happens when the code is executed but for now the only thing I want you to include by default is the __fig.align='center'__ option. You can also insert comments or prevent a piece of code from being executed by using the __#__ symbol within a code-block. 


# Basic Operations in R 
You can execute a large array of commands in R but let us start by using it as a simple calculator. For example, let us do some additions, subtractions, multiplications, divisions, squaring, taking the cube root, etc.



```r
2 + 5 # add 2 and 5
```

```
## [1] 7
```

```r
2 * 5 # multiply 2 and 5
```

```
## [1] 10
```

```r
2/5 # divide 2 by 5
```

```
## [1] 0.4
```

```r
2 - 5 # subract 5 from 2
```

```
## [1] -3
```

```r
(2)^2 # square 2
```

```
## [1] 4
```

```r
(2)^3 # cube 2
```

```
## [1] 8
```

```r
sqrt(4) # take the square-root of 4
```

```
## [1] 2
```

```r
(27)^(1/3) # cube root of 27
```

```
## [1] 3
```


Your calculated values can be stored in __objects__ using either of two  assignment operators, $<-$ or $=$ (preferred). Thus for example, you can create objects as shown below:


```r
x = 29
y = 2
xy = x * y # multiply x and y
```

Once an object has been created you can see what it is by simply typing its name. 


```r
x
```

```
## [1] 29
```

```r
y
```

```
## [1] 2
```

```r
xy
```

```
## [1] 58
```

When naming objects, remember that R is case-sensitive so that it views __X__ and __x__ as two completely different objects. When naming objects there are some things you can/cannot do. 

* You cannot use symbols such as !, +, -, \#.  
* You can use a dot (.), the underscore (\_), and numbers. In fact an object's name can even begin with a dot but a name cannot start with a number. 


# Creating Data in R
It is very easy to generate data in R. For example, let us say I want to create a column of data values that run from 1 to 10, and I want to call this column __x__. I can do this as shown below:


```r
x = c(1:10)
```

Maybe I want to create a second column of 10 data values that start at 100 and increase by 2 (see below):  

```r
y = seq(from=100, to=118, by=2)
```

Now I want to combine these two columns to create a single data-set. 

```r
my.data = as.data.frame(cbind(x, y))
```

Now we have what R calls a data.frame. Think of this is a data file. In creating this, we gave it a name __(my.data)__ and asked that it be created as a data.frame by __binding the two columns x and y__ via the __cbind()__ command. If we wanted to bind the rows instead we would have had to run the following:

```r
my.data2 = as.data.frame(rbind(x, y))
```

Note the difference:  

* cbind() binds the columns and we end up with 10 observations of 2 variables
* rbind() binds the rows and we end up with 2 observations of 10 variables


# Reading Data Used by Whitlock and Schluter 
The book's website has all the data organized by Chapter. If you click on Chapter 2, for example, you will see the data listed along with the number of the in-text example it is used for or by the problem number. These files are in what is called the __csv__ format -- the comma separated variables format. These files are easy to read into R (see below):


```r
tigers = read.csv("http://whitlockschluter.zoology.ubc.ca/wp-content/data/chapter02/chap02e2aDeathsFromTigers.csv", sep=",", header=TRUE)
```

Note the way we did this. I gave the data a name (tigers) and used the __read.csv()__ command. Inside the read.csv() command I specified that the variables are separated by a comma (the __sep=","__ portion of the code), and that the variables had names (that is, the data contain column headings, by specifying __header="TRUE"__). 

If you now click on __tigers__ in the Data window (upper-right pane) you will see what is contained in the file. We have information on what 88 individuals were doing when they were killed by a tiger. Note one interesting thing here: The activities are listed as text not numbers; R can work with text as information just as easily as it can with numbers.

Let us read in a few more data-sets.

```r
birds = read.csv("http://whitlockschluter.zoology.ubc.ca/wp-content/data/chapter02/chap02e2bDesertBirdAbundance.csv", sep=",", header=TRUE)
hemoglobin = read.csv("http://whitlockschluter.zoology.ubc.ca/wp-content/data/chapter02/chap02e3cHumanHemoglobinElevation.csv", sep=",", header=TRUE)
```

If you look at the hemoglobin data you notice that there are 1,962 observations, each from a certain individual in a certain country. How do we know this? Because we opened the data-set and scrolled through it. As a rule you want to always take a quick look at what you have in the data-set. An easy way to do this is by running the __summary()__ command.


```r
summary(tigers)
```

```
##      person                       activity 
##  Min.   : 1.00   Grass/fodder         :44  
##  1st Qu.:22.75   Forest products      :11  
##  Median :44.50   Fishing              : 8  
##  Mean   :44.50   Herding              : 7  
##  3rd Qu.:66.25   Disturbing tiger kill: 5  
##  Max.   :88.00   Fuelwood/timber      : 5  
##                  (Other)              : 8
```

```r
summary(birds)
```

```
##                     species     abundance     
##  American Kestrel       : 1   Min.   :  1.00  
##  Ash-throated Flycatcher: 1   1st Qu.:  3.50  
##  Bell's Vireo           : 1   Median : 18.00  
##  Black Vulture          : 1   Mean   : 74.77  
##  Black-chin. Hummingbird: 1   3rd Qu.:102.50  
##  Black-tail. Gnatcatcher: 1   Max.   :625.00  
##  (Other)                :37
```

```r
summary(hemoglobin)
```

```
##              id         hemoglobin       population  
##  Andean.male1 :   1   Min.   :10.40   Andes   :  71  
##  Andean.male10:   1   1st Qu.:14.80   Ethiopia: 128  
##  Andean.male11:   1   Median :15.45   Tibet   :  59  
##  Andean.male12:   1   Mean   :15.56   USA     :1704  
##  Andean.male13:   1   3rd Qu.:16.15                  
##  Andean.male14:   1   Max.   :25.06                  
##  (Other)      :1956
```

Note how for the hemoglobin data you are shown a variable called __population__ that identifies what region or country an individual came from. You can easily see that the USA has the largest share of the data (1704), followed by Ethiopia (128), then the Andes (71), and finally by Tibet (59). You also see the lowest recorded hemoglobin count is 10.40 and the highest is 25.06. 

You can also see the structure of a data-set if you click on the "play" button before the data. If you do this for hemoglobin you will see the following: 

<img src="Lab_1_files/figure-html/unnamed-chunk-14-1.png" title="" alt="" style="display: block; margin: auto;" />

The variable hemoglobin shows up as "num", short for numeric, indicating that the hemoglobin variable has only numbers. The variable population, on the other hand, is classified as a "Factor" and shown to have four levels. You may think that Factor = text variables but that isn't true. In fact, you could have assigned numbers to the countries and then labeled these numbers. We will see plenty of such examples during the semester.

# Reading Excel Files
There are several R packages that allow you to read Excel files but my personal favorite is the __readxl__ package. You can install this by going to __Tools -> Install Packages ...__ in the RStudio menu. Just type in the package name and you will see it being installed. Once installed, packages become a part of your R/RStudio setup but since they are often updated every few weeks you should check for updates by going to __Tools -> Check for Package Updates ...__ in the RStudio menu.  

Let us read in two Excel files -- __file1.xls__ (an older version of Excel) and __file2.xls__ (the latest version of Excel). You can download these files by clicking on the following links:

* [file1.xls](https://app.box.com/s/v87mm37qfv2to5tvww6bprgkd2pnkmpu)
* [file2.xlsx](https://app.box.com/s/ge5sfpjd1ff80roxub3asyfml54l1fvm)

Note where you saved them (in my case they are on my Desktop). Now set your working directory to point to where the files are, call the readxl package via the __library()__ comand, and then read them in as shown below:


```r
setwd("~/Desktop/")
library(readxl)
file1 = read_excel("file1.xls")
file2 = read_excel("file2.xlsx")
```

# Saving Dataframes in R Format 
Having read in files that were in non-R formats, maybe having modified these files, calculated various things, etc. we may want to save them in native R format. This can be done as follows:

```r
save(tigers, file="tigers.rdata")
```

Note that since we set the working directory this file will be saved to the working directory. 

The next time you want to work with this file you can open it by executing the following command:

```r
load("~/Desktop/tigers.rdata")
```

