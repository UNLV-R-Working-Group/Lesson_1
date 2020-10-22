# Lesson 1: Hello World!

In this lesson we will cover three very basic topics
* Variables and datatypes in R
* Functions, arguments, and keyword arguments
* Dataframes: the bread and butter of data science in R

_Big thanks to Theresa Clark and Cornelia Fanter for offering their expertise to our students during these lessons_

### Variables and datatypes in R
What is a variable? A variable is an object that references some data by a specific name. In this exercise we will learn about how to create a variable, different types of variables, and why we need to understand these basic concepts.

Let's begin by creating our very first variable. After opening Rstudio, type in a name for your variable followed by an equals sign and the value. For now let's use a value of "Hello World". You can use almost any name for your variable, but it is generally good practice to keep it short and descriptive so that you may reference it easily later. You cannot use spaces or special characters ($, #, @, !) in a variable name.

`> message = 'Hello World'`

Here, the text stored in the variable is surrounded by quotes, you can use single quotes or double quotes. Any text inside quotes is considered a 'string' in classical computer science terminology or as a 'character array' in R terminology. This is because the text is stored as an array (or ordered list) of characters. 

Text is not the only type of data we can store in a variable, the _basic_ datatypes are:
* Character `'A string like this'`
* Integer `42`
* Numeric `4.20`
* Logical `TRUE`

Any basic datatype can be stored in an array (or a vector) by using the `c()` function.

`> array_1 = c(1,2,3,4,5)`

`> array_1`

`[1] 1 2 3 4 5`

An element of any vector can be indexed by using brackets like so

`> array_1[3]`

`[1] 3`

Or a range of elements can be indexed by using a colon inside brackets like so

`> array_1[3:5]` 

`[1] 3 4 5`

To access every element **except** one, use negative numbers

`> array_1[-3]`

`[1] 1 2 4 5`

To remove multiple elements, store those negative numbers in a collection

`> array_1[-c(3:5)]`

`[1] 1 2`

What should we do if we don't know the type of a variable? Sometimes it's useful for debugging (and you will be doing a lot of that) to know what the datatype of a variable is. But when we print the variable to the screen, we only get the value, not the type. In the next section we will discuss functions, one of which we can use to display the type of a variable.

### Functions, arguments, and keyword arguments

In this section we will discover functions and how to use them. A function is simply an algorithm that takes some input, usually a variable or several and produces some output. Functions are commands you can type into R, and they are always followed by parenthesis, where the input and other arguments are placed to tell the function what to do. The simplest function is the `print()` function. Try printing our message from earlier

`> print(message)`

`[1] Hello World`

Easy enough, right? In the last section we introduced a function that is called `c()` which turns a collection of data into a vector. The inputs to `c()` are just the elements of the list, and the output is the list itself. Note that in order to store this list, you need to assign it to a variable, otherwise the list will simply be printed to the screen. Try the following two different commands.

`> c(1,2,3,4,5)`

`> array_1 = c(1,2,3,4,5)`

Note how the first prints the values to the screen while the second just creates a new variable. To answer the question posed at the end of the last section, we can use another function called `typeof()` which takes one input, the variable that you want to know the type of. The output is a statement of the datatype printed to the screen. Try it

`> typeof(array_1)`

What happens if you try to store this as a variable? What is the datatype? It says "double", but that's not a datatype we have reviewed yet. The trick here is that some datatypes have a heirarchical structure. All "double" datatypes inherit the "numeric" datatype (or "class" as it is sometimes referred to). Verify this by using the `is.numeric()` function which takes a variable as its input and outputs a boolean or logical value (TRUE/FALSE). This can get very tricky, so here's a [graphic](data-structures-overview.png) that makes all the datatypes in R clear. We won't go too deep into this as it can take a whole session just to teach this thoroughly.

For the next step, you're going to need to download [toy_dataset_1](toy_data_1.csv) from the class github page. Import this data into R by using the following function

`> toy = read.csv('/path/to/file/toy_data_1.csv')`

Make sure to replace the path to your file with the path on your local machine to the toy data file. If you're confused about how to do this, ask an instructor (Theresa, Nell, or Dylan) and they will help you find it. Once you have the data in your R environment, use the `summary()` function to see some statistics about the data. Does anyone know what the skew of this data is based on this information? Note there is one column named 'data' with 1000 entries. For now we will only look at one column in a dataset, but note a dataset can have thousands of columns, which means thousands of variables. We will explore high dimensional datasets at a later date.

Now we will learn about arguments and keyword arguments. To explore this topic, we will primarily be using the `hist()` function on our toy dataset. Arguments are the different inputs you can give to the function, in this case the only required argument is a vector of data. We can produce a histogram of this vector by typing

`> hist(toy$data)`

Note that we have to specify a column, or a vector, within our dataset using the `$` operator. That is because R does not know which column to make the histogram out of unless we tell it, even though there is only one column in this dataset. It is important to know what the argument's datatype needs to be for this reason, and I highly reccomend looking at the documentation for each function you use the first couple times you use it. The docs for `hist()` can be found by googling 'R hist()' or by following this [link](https://www.rdocumentation.org/packages/graphics/versions/3.6.2/topics/hist). Getting familiar with sites like https://www.rdocumentation.org is of the utmost importance and here in the lecture I'd like to take a minute to familiarize you with the layout as it uses common terminology and syntax across many computer science manuals. 

Note that many of the arguments are preceeded by a name and an equals sign like "col = ", these are called keyword arguments (kwargs) and they use a keyword to denote their value. Most of the time these are optional and have default values, but because they use a specific word to denote their presence, we can call them in any order. Let's make our histogram green!

`> hist(toy$data, col = 'green')`

Cool, huh? A couple things to note, each kwarg and its corresponding value are separated by a comma, and the value must be in quotes if it is text. Now, let's see if we can add a title and labels to our axes.

`> hist(toy$data, col = 'green', main = 'Title', xlab = 'x label', ylab = 'y label')`

Take a moment to look through the kwargs on the documentation and play around with your histogram to customize it. Next we will learn about dataframes.

### Dataframes: the bread and butter of data science in R

What happens when you return the type of the data contained in our toy dataset? Though it's not clear from that, but in fact it *is* a dataframe. Dataframes hold vectors, which themselves hold the basic datatypes we talked about at the beginning. Confusing, I know. But we can always check to see if a given variable is a dataframe using the function `is.data.frame()`. Try it on our dataset.

Dataframes are the objects that hold most of the data in R. Every time you import data from an Excel spreadsheet it will be imported as a datafram in R. There's a *ton* of functionality built into dataframes, and we will only touch on a few for this lecture. For the next section, you'll need to download [toy_dataset_2](toy_data_2.csv) and import it into your R session just like we did before, but this time replacing the path with the path to the new dataset. 

`> toy2 = read.csv('/path/to/file/toy_data_2.csv')`

Let's get a quick view of the data by using the `summary()` function. What are the variable names, and datatypes of each of them? Print the first few rows of the dataframe by using the `head()` function to get a visual of what our data looks like. Each row can be thought of as one data point, or if you're more familiar with clinical data, one subject. Each row contains three variables, each a measurement of the data point. Let's take a look at the distribution of one variable.

For those that have R Version 4.0.2, the `summary()` function will be slightly different for categorical data. Instead use the `table()` function to see the distribution of the categories.

 `> table(toy2$v3)`
 
 `cyan  green    red yellow` 
 
   `250    250    250    250 `

Access a column with the `$` operator followed by the name of the column you wish to access

`> hist(toy2$v1)`

Access the first 20 rows of this variable by using square brackets following the variable name

`> toy2$v2[1:20]`

It is also possible to index columns by their number. An equivalent command to the previous command would be 

`> toy2[1:20, 2]`

Leaving either row or columns indices blank will return all rows or columns respectively. To return the first 20 rows of all three variables use this command

`> toy2[1:20, ]`

But we can also index based on a conditional statement, which proves very useful when dealing with high dimensional datasets. There are a few operators we need to understand before we get into conditional statements though. The basic ones you will likely need to know are:
* `<` means less than 
* `>` means greater than
* `==` means exactly equal to
* `|` means "OR"
* `&` means "AND"

Let's put this to use in our dataset. Select just the portion of the dataframe that has "green" in the third column with the following command. You can read this command as "the rows of toy2 where v3 in toy2 is equal to 'green'". Note that we want just the rows that match the condition, and all the columns.

`> toy2[toy2$v3=='green', ]` 

How many values does this return? Use the `dim()` function to find out. Does this match the number we got when we got a summary at the beginning? Look at the histogram of v2, around what integer is the mean of this normal distribution? Let's select only the bottom half of this distribution using the following command. Note the column number!

`> toy2[toy2$v2 < 20, 2]`

How many values does this return? Does the histogram of these values look like the left half of a normal distribution? What if we wanted to combine our searches to produce only the bottom half of v2 that are labeled "green" in v3? Use the following command to find out. Note that the conditions are grouped by using parentheses.

`> toy2[(toy2$v2 < 20) & (toy2$v3=='green'), ]`

You might notice how powerful this tool can be already, as an exercise produce a dataframe with all three variables but only containing rows labeled 'red' or 'cyan' in the third column. Then check your work using the `dim()` function.


### Summary
Today we learned the basics of functions, arguments, dataframes, and datatypes. Next week we will start learning more about practical applications of R by doing basic statistical analysis on more toy data. Hope you all enjoyed this little learning session!


