# Lesson 1: Hello World!

In this lesson we will cover three very basic topics
* Variables and datatypes in R
* Functions, arguments, and keyword arguments
* Dataframes: the bread and butter of data science in R

### Variables and datatypes in R
What is a variable? A variable is an object that references some data by a specific name. In this exercise we will learn about how to create a variable, different types of variables, and why we need to understand these basic concepts.

Let's begin by creating our very first variable. After opening Rstudio, type in a name for your variable followed by an equals sign and the value. For now let's use a value of "Hello World". You can use almost any name for your variable, but it is generally good practice to keep it short and descriptive so that you may reference it easily later. You cannot use spaces or special characters ($, #, @, !) in a variable name.

`> message = 'Hello World'`

Here, the text stored in the variable is surrounded by quotes, you can use single quotes or double quotes. Any text inside quotes is considered a 'string' in classical computer science terminology or as a 'character array' in R terminology. This is because the text is stored as an array (or ordered list) of characters. 

Text is not the only type of data we can store in a variable, the basic datatypes are:
* Character `'A string like this'`
* Integer `42`
* Numeric `4.20`
* Logical `True`

Any basic datatype can be stored in an array by using the `c()` function.

`> array_1 = c(1,2,3,4,5)`

`> array_1`

`[1] 1 2 3 4 5`

An element of any array can be indexed by using brackets like so

`> array_1[3]`

`[1] 3`

Or a range of elements can be indexed by using a colon inside brackets like so

`> array_1[3:5]` 

`[1] 3 4 5`

To access every element **except** one, use negative numbers

`> array_1[-3]`

`[1] 1 2 4 5`

What should we do if we don't know the type of a variable? Sometimes it's useful for debugging (and you will be doing a lot of that) to know what the datatype of a variable is. But when we print the variable to the screen, we only get the value, not the type. In the next section we will discuss functions, one of which we can use to display the type of a variable.

### Functions, arguments, and keyword arguments

In this section we will discover functions and how to use them. A function is simply an algorithm that takes some input, usually a variable or several and produces some output. Functions are commands you can type into R, and they are always followed by parenthesis, where the input and other arguments are placed to tell the function what to do. The simplest function is the `print()` function. Try printing our message from earlier

`> print(message)`

`[1] Hello World`

Easy enough, right? In the last section we introduced a function that is called `c()` which turns a collection of data into an array. The inputs to `c()` are just the elements of the list, and the output is the list itself. Note that in order to store this list, you need to assign it to a variable, otherwise the list will simply be printed to the screen. Try the following two different commands.

`> c(1,2,3,4,5)`

`> array_1 = c(1,2,3,4,5)`

Note how the first prints the values to the screen while the second just creates a new variable. To answer the question posed at the end of the last section, we can use another function called `typeof()` which takes one input, the variable that you want to know the type of. The output is a statement of the datatype printed to the screen. Try it

`> typeof(array_1)`

What happens if you try to store this as a variable? What is the datatype? It says "double", but that's not a datatype we have reviewed yet. The trick here is that some datatypes have a heirarchical structure. All "double" datatypes inherit the "numeric" datatype (or "class" as it is sometimes referred to). Verify this by using the `is.numeric()` function which takes a variable as its input and outputs a boolean or logical value (TRUE/FALSE). This can get very tricky, so here's a [graphic](data-structures-overview.png) that makes all the datatypes clear. We won't go too deep into this as it can take a whole session just to teach this thoroughly.




