Reading Help files
------------------

R, and every package, provide help files for functions. To search for help on a function from a specific function that is in a package loaded into your namespace (your interactive R session):

    ?function_name
    help(function_name)

{: .r}

This will load up a help page in RStudio (or as plain text in R by itself).

Each help page is broken down into sections:

-   Description: An extended description of what the function does.
-   Usage: The arguments of the function and their default values.
-   Arguments: An explanation of the data each argument is expecting.
-   Details: Any important details to be aware of.
-   Value: The data the function returns.
-   See Also: Any related functions you might find useful.
-   Examples: Some examples for how to use the function.

Different functions might have different sections, but these are the main ones you should be aware of.

> Tip: Reading help files
> -----------------------
>
> One of the most daunting aspects of R is the large number of functions available. It would be prohibitive, if not impossible to remember the correct usage for every function you use. Luckily, the help files mean you don't have to! {: .callout}

Special Operators
-----------------

To seek help on special operators, use quotes:

    ?"+"

{: .r}

Getting help on packages
------------------------

Many packages come with "vignettes": tutorials and extended example documentation. Without any arguments, `vignette()` will list all vignettes for all installed packages; `vignette(package="package-name")` will list all available vignettes for `package-name`, and `vignette("vignette-name")` will open the specified vignette.

If a package doesn't have any vignettes, you can usually find help by typing `help("package-name")`.

When you kind of remember the function
--------------------------------------

If you're not sure what package a function is in, or how it's specifically spelled you can do a fuzzy search:

    ??function_name

{: .r}

When you have no idea where to begin
------------------------------------

If you don't know what function or package you need to use [CRAN Task Views](http://cran.at.r-project.org/web/views) is a specially maintained list of packages grouped into fields. This can be a good starting point.

When your code doesn't work: seeking help from your peers
---------------------------------------------------------

If you're having trouble using a function, 9 times out of 10, the answers you are seeking have already been answered on [Stack Overflow](http://stackoverflow.com/). You can search using the `[r]` tag.

If you can't find the answer, there are a few useful functions to help you ask a question from your peers:

    ?dput

{: .r}

Will dump the data you're working with into a format so that it can be copy and pasted by anyone else into their R session.

    sessionInfo()

{: .r}

    R version 3.3.2 (2016-10-31)
    Platform: x86_64-apple-darwin13.4.0 (64-bit)
    Running under: macOS Sierra 10.12.5

    locale:
    [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

    attached base packages:
    [1] stats     graphics  grDevices utils     datasets  methods   base     

    other attached packages:
    [1] knitr_1.14

    loaded via a namespace (and not attached):
     [1] backports_1.0.5 magrittr_1.5    rprojroot_1.2   formatR_1.4    
     [5] tools_3.3.2     htmltools_0.3.5 yaml_2.1.13     Rcpp_0.12.7    
     [9] stringi_1.1.1   rmarkdown_1.3   stringr_1.1.0   digest_0.6.10  
    [13] evaluate_0.9   

{: .output}

Will print out your current version of R, as well as any packages you have loaded. This can be useful for others to help reproduce and debug your issue.

> Challenge 1
> -----------
>
> Look at the help for the `c` function. What kind of vector do you expect you will create if you evaluate the following:
>
>     c(1, 2, 3)
>     c('d', 'e', 'f')
>     c(1, 2, 'f')
>
> {: .r} &gt; \#\# Solution to Challenge 1 &gt; &gt; The `c()` function creates a vector, in which all elements are the &gt; same type. In the first case, the elements are numeric, in the &gt; second, they are characters, and in the third they are characters: &gt; the numeric values are "coerced" to be characters. {: .solution} {: .challenge}

> Challenge 2
> -----------
>
> Look at the help for the `paste` function. You'll need to use this later. What is the difference between the `sep` and `collapse` arguments?
>
> > Solution to Challenge 2
> > -----------------------
> >
> > To look at the help for the `paste()` function, use:
> >
> >     help("paste")
> >     ?paste
> >
> > {: .r} The difference between `sep` and `collapse` is a little tricky. The `paste` function accepts any number of arguments, each of which can be a vector of any length. The `sep` argument specifies the string used between concatenated terms — by default, a space. The result is a vector as long as the longest argument supplied to `paste`. In contrast, `collapse` specifies that after concatenation the elements are *collapsed* together using the given separator, the result being a single string. e.g.
> >
> >     paste(c("a","b"), "c")
> >
> > {: .r}
> >
> >     [1] "a c" "b c"
> >
> > {: .output}
> >
> >     paste(c("a","b"), "c", sep = ",")
> >
> > {: .r}
> >
> >     [1] "a,c" "b,c"
> >
> > {: .output}
> >
> >     paste(c("a","b"), "c", collapse = "|")
> >
> > {: .r}
> >
> >     [1] "a c|b c"
> >
> > {: .output}
> >
> >     paste(c("a","b"), "c", sep = ",", collapse = "|")
> >
> > {: .r}
> >
> >     [1] "a,c|b,c"
> >
> > {: .output} (For more information, scroll to the bottom of the `?paste` help page and look at the examples, or try `example('paste')`.) {: .solution} {: .challenge}

> Challenge 3
> -----------
>
> Use help to find a function (and its associated parameters) that you could use to load data from a csv file in which columns are delimited with "" (tab) and the decimal point is a "." (period). This check for decimal separator is important, especially if you are working with international colleagues, because different countries have different conventions for the decimal point (i.e. comma vs period). hint: use `??csv` to lookup csv related functions. &gt; \#\# Solution to Challenge 3 &gt; &gt; The standard R function for reading tab-delimited files with a period &gt; decimal separator is read.delim(). You can also do this with &gt; `read.table(file, sep="\t")` (the period is the *default* decimal &gt; separator for `read.table()`, although you may have to change &gt; the `comment.char` argument as well if your data file contains &gt; hash (\#) characters {: solution} {: .challenge}

Other ports of call
-------------------

-   [Quick R](http://www.statmethods.net/)
-   [RStudio cheat sheets](http://www.rstudio.com/resources/cheatsheets/)
-   [Cookbook for R](http://www.cookbook-r.com/)