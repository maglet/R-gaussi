---
title: "Exploring Data Frames"
teaching: 30
exercises: 20
questions:
- "How can I get to know the structure a data frame?"
- "How can I work with subsets of data in R?"
objectives:
- "Be able to find basic properties of a data frames including size, class or type of the columns, names, and first few rows."
- "Be able to articulate what a `factor` is and how to convert between `factor` and `character`."
- "To be able to subset data frames"
- "To be able to extract individual and multiple elements by index, by name, using comparison operations"
- "To be able to skip and remove elements from various data structures."

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

> ## Challenge
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

Subetting lets you select a single data element or separate based on a factor. For example, what if you want all of the data concerning countries in Asia in the gapminder dataset. 


There are three ways to subset: by index, by name and by logical operators. Let's look at subsetting by index first. 

### Accessing elements using their indices

To simplify things, only look at one column of the data frame: `lifeExp`. From `str`, we know that it's the fifth column in the data frame. 

To load the `lifeExp` column into a new variable x: 


~~~
x<-lifeExp[,5]
~~~
{: .r}



~~~
Error in eval(expr, envir, enclos): object 'lifeExp' not found
~~~
{: .error}

That means we want all of the fifth column loaded into x. Let's say we want to pick out the third element of x:


~~~
x[3]
~~~
{: .r}



~~~
[1] NA
~~~
{: .output}

We can ask for multiple elements at once. This coke picks out the first and third elements using the `c`, or concatenate, function. `c` creates a vector of numbers that can be used for subsetting.


~~~
x[c(1, 3)]
~~~
{: .r}



~~~
[1] "_episodes_rmd/02-data-frames.Rmd" NA                                
~~~
{: .output}

We can also ask for slices of the vector using the `:` operator. The following code makes a vector of all numbers 1-4, and hence the first 4 elements of x.


~~~
x[1:4]
~~~
{: .r}



~~~
[1] "_episodes_rmd/02-data-frames.Rmd" NA                                
[3] NA                                 NA                                
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

## Subsetting by name

We can extract elements by using their name, instead of index:


~~~
x[c("a", "c")]
~~~
{: .r}



~~~
[1] NA NA
~~~
{: .output}

This is usually a much more reliable way to subset objects: the
position of various elements can often change when chaining together
subsetting operations, but the names will always remain the same!

> ## Tip: Getting help for operators
>
> Remember you can search for help on operators by wrapping them in quotes:
> `help(":")` or `?":"`.
>
{: .callout}

## Subsetting through other logical operations

We can also more simply subset through logical operations:


~~~
x[c(TRUE, TRUE, FALSE, FALSE)]
~~~
{: .r}



~~~
[1] "_episodes_rmd/02-data-frames.Rmd" NA                                
~~~
{: .output}

Note that in this case, the logical vector is also recycled to the
length of the vector we're subsetting!


~~~
x[c(TRUE, FALSE)]
~~~
{: .r}



~~~
[1] "_episodes_rmd/02-data-frames.Rmd"
~~~
{: .output}

Since comparison operators evaluate to logical vectors, we can also
use them to succinctly subset vectors:


~~~
x[x > 7]
~~~
{: .r}



~~~
character(0)
~~~
{: .output}

> ## Tip: Combining logical conditions
>
> There are many situations in which you will wish to combine multiple logical
> criteria. For example, we might want to find all the countries that are
> located in Asia **or** Europe **and** have life expectancies within a certain
> range. Several operations for combining logical vectors exist in R:
>
>  * `&`, the "logical AND" operator: returns `TRUE` if both the left and right
>    are `TRUE`.
>  * `|`, the "logical OR" operator: returns `TRUE`, if either the left or right
>    (or both) are `TRUE`.
>
> The recycling rule applies with both of these, so `TRUE & c(TRUE, FALSE, TRUE)`
> will compare the first `TRUE` on the left of the `&` sign with each of the
> three conditions on the right.
>
> You may sometimes see `&&` and `||` instead of `&` and `|`. These operators
> do not use the recycling rule: they only look at the first element of each
> vector and ignore the remaining elements. The longer operators are mainly used
> in programming, rather than data analysis.
>
>  * `!`, the "logical NOT" operator: converts `TRUE` to `FALSE` and `FALSE` to
>    `TRUE`. It can negate a single logical condition (eg `!TRUE` becomes
>    `FALSE`), or a whole vector of conditions(eg `!c(TRUE, FALSE)` becomes
>    `c(FALSE, TRUE)`).
>
> Additionally, you can compare the elements within a single vector using the
> `all` function (which returns `TRUE` if every element of the vector is `TRUE`)
> and the `any` function (which returns `TRUE` if one or more elements of the
> vector are `TRUE`).
{: .callout}

> ## Challenge 3
>
> Given the gapminder dataset, write a subsetting command to return the values > that are greater than 30 and less than 60.
>
> > ## Solution to challenge 3
> >
> > 
> > ~~~
> > x_subset <- x[x<40 & x>60]
> > print(x_subset)
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > ~~~
> > character(0)
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## Handling special values

At some point you will encounter functions in R which cannot handle missing, infinite,
or undefined data.

There are a number of special functions you can use to filter out this data:

 * `is.na` will return all positions in a vector, matrix, or data.frame
   containing `NA`.
 * likewise, `is.nan`, and `is.infinite` will do the same for `NaN` and `Inf`.
 * `is.finite` will return all positions in a vector, matrix, or data.frame
   that do not contain `NA`, `NaN` or `Inf`.
 * `na.omit` will filter out all missing values from a vector

## Factor subsetting

Now that we've explored the different ways to subset vectors, how
do we subset the other data structures?

Factor subsetting works the same way as vector subsetting.


~~~
f <- gapminder$Continent
f[f == "Asia"]
~~~
{: .r}



~~~
NULL
~~~
{: .output}



~~~
f[1:3]
~~~
{: .r}



~~~
NULL
~~~
{: .output}

## Data frames

Remember the data frames are lists underneath the hood, so similar rules
apply. However they are also two dimensional objects:

`[` with one argument will select the third column. The resulting object will be a data frame:


~~~
head(gapminder[3])
~~~
{: .r}



~~~
       pop
1  8425333
2  9240934
3 10267083
4 11537966
5 13079460
6 14880372
~~~
{: .output}

Similarly, `[[` will act to extract *a single column*:


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

With two arguments, `[` behaves the same way as for matrices:


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

If we subset a single row, the result will be a data frame (because
the elements are mixed types):


~~~
gapminder[3,]
~~~
{: .r}



~~~
      country year      pop continent lifeExp gdpPercap
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
~~~
{: .output}

But for a single column the result will be a vector (this can
be changed with the third argument, `drop = FALSE`).

> ## Challenge 7
>
> Fix each of the following common data frame subsetting errors:
>
> 1. Extract observations collected for the year 1957
>
>    
>    ~~~
>    gapminder[gapminder$year = 1957,]
>    ~~~
>    {: .r}
>
> 2. Extract all columns except 1 through to 4
>
>    
>    ~~~
>    gapminder[,-1:4]
>    ~~~
>    {: .r}
>
> 3. Extract the rows where the life expectancy is longer the 80 years
>
>    
>    ~~~
>    gapminder[gapminder$lifeExp > 80]
>    ~~~
>    {: .r}
>
> 4. Extract the first row, and the fourth and fifth columns
>   (`lifeExp` and `gdpPercap`).
>
>    
>    ~~~
>    gapminder[1, 4, 5]
>    ~~~
>    {: .r}
>
> 5. Advanced: extract rows that contain information for the years 2002
>    and 2007
>
>    
>    ~~~
>    gapminder[gapminder$year == 2002 | 2007,]
>    ~~~
>    {: .r}
>
> > ## Solution to challenge 7
> >
> > Fix each of the following common data frame subsetting errors:
> >
> > 1. Extract observations collected for the year 1957
> >
> >    
> >    ~~~
> >    # gapminder[gapminder$year = 1957,]
> >    gapminder[gapminder$year == 1957,]
> >    ~~~
> >    {: .r}
> >
> >
> > 3. Extract the rows where the life expectancy is longer the 80 years
> >
> >    
> >    ~~~
> >    # gapminder[gapminder$lifeExp > 80]
> >    gapminder[gapminder$lifeExp > 80,]
> >    ~~~
> >    {: .r}
> >
> > 4. Extract the first row, and the fourth and fifth columns
> >   (`lifeExp` and `gdpPercap`).
> >
> >    
> >    ~~~
> >    # gapminder[1, 4, 5]
> >    gapminder[1, c(4, 5)]
> >    ~~~
> >    {: .r}
> >
> > 5. Advanced: extract rows that contain information for the years 2002
> >    and 2007
> >
> >     
> >     ~~~
> >     # gapminder[gapminder$year == 2002 | 2007,]
> >     gapminder[gapminder$year == 2002 | gapminder$year == 2007,]
> >     gapminder[gapminder$year %in% c(2002, 2007),]
> >     ~~~
> >     {: .r}
> {: .solution}
{: .challenge}

> ## Challenge 8
>
> 1. Why does `gapminder[1:20]` return an error? How does it differ from `gapminder[1:20, ]`?
>
>
> 2. Create a new `data.frame` called `gapminder_small` that only contains rows 1 through 9
> and 19 through 23. You can do this in one or two steps.
>
> > ## Solution to challenge 8
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
