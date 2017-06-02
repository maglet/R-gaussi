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


## Subsetting through other logical operations

We can also more simply subset through logical operations. To illustrate, let's make a vector called n10 that contains integers 1 through 10.


~~~
n10<-1:10
~~~
{: .r}

Let's subset the odd numbers using `TRUE` and `FALSE`. 


~~~
n10[c(TRUE, FALSE, TRUE, FALSE, TRUE, FALSE,TRUE, FALSE, TRUE, FALSE)]
~~~
{: .r}



~~~
[1] 1 3 5 7 9
~~~
{: .output}

Pretty neat, huh? We can do this even more simply because,  the logical vector is also recycled to the length of the vector we're subsetting!


~~~
n10[c(TRUE, FALSE)]
~~~
{: .r}



~~~
[1] 1 3 5 7 9
~~~
{: .output}

### Using logical operators
Since comparison operators evaluate to logical vectors, we can also
use them to succinctly subset vectors. Let's find countries with a life expectancy greater than 80 years.


~~~
gapminder[gapminder$lifeExp > 80, ]
~~~
{: .r}



~~~
             country year       pop continent lifeExp gdpPercap
71         Australia 2002  19546792   Oceania  80.370  30687.75
72         Australia 2007  20434176   Oceania  81.235  34435.37
252           Canada 2007  33390141  Americas  80.653  36319.24
540           France 2007  61083916    Europe  80.657  30470.02
671  Hong Kong China 2002   6762476      Asia  81.495  30209.02
672  Hong Kong China 2007   6980412      Asia  82.208  39724.98
695          Iceland 2002    288030    Europe  80.500  31163.20
696          Iceland 2007    301931    Europe  81.757  36180.79
768           Israel 2007   6426679      Asia  80.745  25523.28
779            Italy 2002  57926999    Europe  80.240  27968.10
780            Italy 2007  58147733    Europe  80.546  28569.72
802            Japan 1997 125956499      Asia  80.690  28816.58
803            Japan 2002 127065841      Asia  82.000  28604.59
804            Japan 2007 127467972      Asia  82.603  31656.07
1104     New Zealand 2007   4115771   Oceania  80.204  25185.01
1152          Norway 2007   4627926    Europe  80.196  49357.19
1428           Spain 2007  40448191    Europe  80.941  28821.06
1475          Sweden 2002   8954175    Europe  80.040  29341.63
1476          Sweden 2007   9031088    Europe  80.884  33859.75
1487     Switzerland 2002   7361757    Europe  80.620  34480.96
1488     Switzerland 2007   7554661    Europe  81.701  37506.42
~~~
{: .output}

#### Factor subsetting

Factor subsetting works the same way as vector subsetting. Let's look for records of countries in Oceania.


~~~
gapminder[gapminder$continent == "Oceania",]
~~~
{: .r}



~~~
         country year      pop continent lifeExp gdpPercap
61     Australia 1952  8691212   Oceania  69.120  10039.60
62     Australia 1957  9712569   Oceania  70.330  10949.65
63     Australia 1962 10794968   Oceania  70.930  12217.23
64     Australia 1967 11872264   Oceania  71.100  14526.12
65     Australia 1972 13177000   Oceania  71.930  16788.63
66     Australia 1977 14074100   Oceania  73.490  18334.20
67     Australia 1982 15184200   Oceania  74.740  19477.01
68     Australia 1987 16257249   Oceania  76.320  21888.89
69     Australia 1992 17481977   Oceania  77.560  23424.77
70     Australia 1997 18565243   Oceania  78.830  26997.94
71     Australia 2002 19546792   Oceania  80.370  30687.75
72     Australia 2007 20434176   Oceania  81.235  34435.37
1093 New Zealand 1952  1994794   Oceania  69.390  10556.58
1094 New Zealand 1957  2229407   Oceania  70.260  12247.40
1095 New Zealand 1962  2488550   Oceania  71.240  13175.68
1096 New Zealand 1967  2728150   Oceania  71.520  14463.92
1097 New Zealand 1972  2929100   Oceania  71.890  16046.04
1098 New Zealand 1977  3164900   Oceania  72.220  16233.72
1099 New Zealand 1982  3210650   Oceania  73.840  17632.41
1100 New Zealand 1987  3317166   Oceania  74.320  19007.19
1101 New Zealand 1992  3437674   Oceania  76.330  18363.32
1102 New Zealand 1997  3676187   Oceania  77.550  21050.41
1103 New Zealand 2002  3908037   Oceania  79.110  23189.80
1104 New Zealand 2007  4115771   Oceania  80.204  25185.01
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
> Given the gapminder dataset, write a subsetting command to return the values
> that are greater than 30 and less than 60.
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
> > numeric(0)
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Challenge 4
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
> 2. Extract the rows where the gdp per capita is greater than 30000
>
>    
>    ~~~
>    gapminder[gapminder$gdp > 30000]
>    ~~~
>    {: .r}
>
> 3. Extract the first row, and the fourth and fifth columns
>   (`lifeExp` and `gdpPercap`).
>
>    
>    ~~~
>    gapminder[1, 4, 5]
>    ~~~
>    {: .r}
>
> 4. Advanced: extract rows that contain information for the years 2002
>    and 2007
>
>    
>    ~~~
>    gapminder[gapminder$year == 2002 | 2007,]
>    ~~~
>    {: .r}
>
> > ## Solution to challenge 4
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
> > 2. Extract the rows where the life expectancy is longer the 80 years
> >
> >    
> >    ~~~
> >    # gapminder[gapminder$lifeExp > 80]
> >    gapminder[gapminder$lifeExp > 80,]
> >    ~~~
> >    {: .r}
> >
> > 3. Extract the first row, and the fourth and fifth columns
> >   (`lifeExp` and `gdpPercap`).
> >
> >    
> >    ~~~
> >    # gapminder[1, 4, 5]
> >    gapminder[1, c(4, 5)]
> >    ~~~
> >    {: .r}
> >
> > 4. Advanced: extract rows that contain information for the years 2002
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
