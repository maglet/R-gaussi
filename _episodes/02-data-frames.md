---
title: "Exploring Data Frames"
teaching: 20
exercises: 10
questions:
- "How can I get to know the structure a data frame?"
- "How can I work with subsets of data in R?"
objectives:
- "Be able to find basic properties of a data frames including size, class or type of the columns, names, and first few rows."
- "Be able to articulate what a `factor` is and how to convert between `factor` and `character`."
- "To be able to subset data frames"
- "To be able to extract individual and multiple elements by index, by name, using comparison operations"

keypoints:
- "Read in a csv file using `read.csv()`"
- "Use `str()`, `nrow()`, `ncol()`, `dim()`, `colnames()`, `rownames()`, `head()` and `typeof()` to understand structure of the data frame"
- "Understand `length()` of a data frame"
- "Use `levels()` and `as.character()` to explore and manipulate factors"
- "Access individual values by location using `[]`."
- "Access slices of data using `[low:high]`."
- "Access arbitrary sets of data using `[c(...)]`."

source: Rmd
---



In this lesson, we'll learn about working with data frames using the gapminder
dataset in your R project folder:

To load the data table into an R variable, use the `read.csv` function.


~~~
gapminder <- read.csv("data/gapminder-FiveYearData.csv")
~~~
{: .r}

Let's investigate gapminder a bit; the first thing we should always do is check out what the data looks like with `str`:


~~~
str(gapminder)
~~~
{: .r}



~~~
'data.frame':	1704 obs. of  6 variables:
 $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop      : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
 $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap: num  779 821 853 836 740 ...
~~~
{: .output}

We can also examine individual columns of the data frame with our `typeof` function:


~~~
typeof(gapminder$year)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
typeof(gapminder$country)
~~~
{: .r}



~~~
[1] "integer"
~~~
{: .output}



~~~
str(gapminder$country)
~~~
{: .r}



~~~
 Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
~~~
{: .output}

We can also interrogate the data frame for information about its dimensions;
remembering that `str(gapminder)` said there were 1704 observations of 6
variables in gapminder, what do you think the following will produce, and why?


~~~
length(gapminder)
~~~
{: .r}



~~~
[1] 6
~~~
{: .output}

A fair guess would have been to say that the length of a data frame would be the
number of rows it has (1704), but this is not the case; remember, a data frame
is a *list of vectors and factors*:


~~~
typeof(gapminder)
~~~
{: .r}



~~~
[1] "list"
~~~
{: .output}

When `length` gave us 6, it's because gapminder is built out of a list of 6
columns. To get the number of rows and columns in our dataset, try:


~~~
nrow(gapminder)
~~~
{: .r}



~~~
[1] 1704
~~~
{: .output}



~~~
ncol(gapminder)
~~~
{: .r}



~~~
[1] 6
~~~
{: .output}

Or, both at once:


~~~
dim(gapminder)
~~~
{: .r}



~~~
[1] 1704    6
~~~
{: .output}

We'll also likely want to know what the titles of all the columns are, so we can
ask for them later:


~~~
colnames(gapminder)
~~~
{: .r}



~~~
[1] "country"   "year"      "pop"       "continent" "lifeExp"   "gdpPercap"
~~~
{: .output}

At this stage, it's important to ask ourselves if the structure R is reporting
matches our intuition or expectations; do the basic data types reported for each
column make sense? If not, we need to sort any problems out now before they turn
into bad surprises down the road, using what we've learned about how R
interprets data, and the importance of *strict consistency* in how we record our
data.

Once we're happy that the data types and structures seem reasonable, it's time
to start digging into our data proper. Check out the first few lines:


~~~
head(gapminder)
~~~
{: .r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
4 Afghanistan 1967 11537966      Asia  34.020  836.1971
5 Afghanistan 1972 13079460      Asia  36.088  739.9811
6 Afghanistan 1977 14880372      Asia  38.438  786.1134
~~~
{: .output}

To make sure our analysis is reproducible, we should put the code
into a script file so we can come back to it later.

> ## Challenge 1
>
> Read the output of `str(gapminder)` again;
> this time, use what you've learned about factors, lists and vectors,
> as well as the output of functions like `colnames` and `dim`
> to explain what everything that `str` prints out for gapminder means.
> If there are any parts you can't interpret, discuss with your neighbors!
>
> > ## Solution to Challenge
> >
> > The object `gapminder` is a data frame with columns
> > - `country` and `continent` are factors.
> > - `year` is an integer vector.
> > - `pop`, `lifeExp`, and `gdpPercap` are numeric vectors.
> >
> {: .solution}
{: .challenge}

## Subsetting

There are many instances where you want to use only a part of a dataset instead of the whole thing. That's where **subsetting** comes in. R has many powerful subset operators and mastering them will allow you to
easily perform complex operations on any kind of dataset. 

Subsetting lets you select a single data element or separate based on a factor. For example, what if you want all of the data concerning countries in Asia in the gapminder dataset. 


There are three ways to subset: by index, by name and by logical operators. Let's look at subsetting by index first. 

### Accessing elements using their indices

To simplify things, only look at one column of the data frame: `lifeExp`. From `str`, we know that it's the fifth column in the data frame. 

To load the `lifeExp` column into a new variable x: 


~~~
x<-gapminder[,5]
~~~
{: .r}

That means we want all of the fifth column loaded into x. Let's say we want to pick out the third element of x:


~~~
x[3]
~~~
{: .r}



~~~
[1] 31.997
~~~
{: .output}

We can ask for multiple elements at once using the `c`, or concatenate, function. `c` creates a vector of numbers that can be used for subsetting. For example, the following code creates a vector with the numbers 1 and 3 in it.


~~~
c(1,3)
~~~
{: .r}



~~~
[1] 1 3
~~~
{: .output}

We can use this vector inside the square brackets after x to get the first and third elements.

~~~
x[c(1, 3)]
~~~
{: .r}



~~~
[1] 28.801 31.997
~~~
{: .output}

We can also ask for slices of the vector using the `:` operator.


~~~
x[1:4]
~~~
{: .r}



~~~
[1] 28.801 30.332 31.997 34.020
~~~
{: .output}

the `:` operator creates a sequence of numbers from the left element to the right. 

~~~
1:4
~~~
{: .r}



~~~
[1] 1 2 3 4
~~~
{: .output}

You can use the `c` function to do something similar

~~~
c(1, 2, 3, 4)
~~~
{: .r}



~~~
[1] 1 2 3 4
~~~
{: .output}

If we ask for a number outside of the vector, R will return missing values:


~~~
x[1800]
~~~
{: .r}



~~~
[1] NA
~~~
{: .output}

### Data Frames

Let's see how this subsetting thing works with whole data frames:

1. An index between single brackets selects a column


~~~
head(gapminder[1])
~~~
{: .r}



~~~
      country
1 Afghanistan
2 Afghanistan
3 Afghanistan
4 Afghanistan
5 Afghanistan
6 Afghanistan
~~~
{: .output}

2. If you want to select a single data point, you use ["row", "column"] format. The following selects the third row in the first column.


~~~
head(gapminder[3,1])
~~~
{: .r}



~~~
[1] Afghanistan
142 Levels: Afghanistan Albania Algeria Angola Argentina ... Zimbabwe
~~~
{: .output}

3. What if you want to select an entire row? Keep the comma, but remove the number specifying the column 


~~~
gapminder[3,]
~~~
{: .r}



~~~
      country year      pop continent lifeExp gdpPercap
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
~~~
{: .output}

4. This works similarly if you want to select one column, but it's kind of redundant with #1 above.


~~~
head(gapminder[,1])
~~~
{: .r}



~~~
[1] Afghanistan Afghanistan Afghanistan Afghanistan Afghanistan Afghanistan
142 Levels: Afghanistan Albania Algeria Angola Argentina ... Zimbabwe
~~~
{: .output}

5. You can use the `c` function, and the `:` operator just like with a single column


~~~
gapminder[1:3,]
~~~
{: .r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
~~~
{: .output}



~~~
gapminder[c(1,3),]
~~~
{: .r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
~~~
{: .output}

> ## Tip: Getting help for operators
>
> Remember you can search for help on operators by wrapping them in quotes:
> `help(":")` or `?":"`.
>
{: .callout}

> ## Challenge 2
>
> 1. Why does `gapminder[1:20]` return an error? How does it differ from `gapminder[1:20, ]`?
>
>
> 2. Create a new `data.frame` called `gapminder_small` that only contains rows 1 through 9
> and 19 through 23. You can do this in one or two steps.
>
> > ## Solution to challenge 2
> >
> > 1.  `gapminder` is a data.frame so needs to be subsetted on two dimensions. `gapminder[1:20, ]` subsets the data to give the first 20 rows and all columns.
> >
> > 2. 
> >
> > 
> > ~~~
> > gapminder_small <- gapminder[c(1:9, 19:23),]
> > ~~~
> > {: .r}
> {: .solution}
{: .challenge}

## Subsetting by name

We can extract elements by using their name, instead of index.

This is usually a much more reliable way to subset objects: the
position of various elements can often change when chaining together
subsetting operations, but the names will always remain the same!

`[[` will act to extract *a single column*:


~~~
head(gapminder[["lifeExp"]])
~~~
{: .r}



~~~
[1] 28.801 30.332 31.997 34.020 36.088 38.438
~~~
{: .output}

And `$` provides a convenient shorthand to extract columns by name:


~~~
head(gapminder$year)
~~~
{: .r}



~~~
[1] 1952 1957 1962 1967 1972 1977
~~~
{: .output}
