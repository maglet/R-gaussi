---
title: "Seeking Help"
teaching: 10
exercises: 0
questions:
- "How can I get help in R?"
objectives:
- "To be able read R help files for functions and special operators."
- "To be able to use CRAN task views to identify packages to solve a problem."
- "To be able to seek help from your peers."
keypoints:
- "Use `help()` to get online help in R."
source: Rmd
output:
  md_document:
    variant: markdown_github
---



## Reading Help files

R, and every package, provide help files for functions. To search for help on a
function from a specific function that is in a package loaded into your
namespace (your interactive R session):


~~~
?function_name
help(function_name)
~~~
{: .r}

This will load up a help page in RStudio (or as plain text in R by itself).

Each help page is broken down into sections:

 - Description: An extended description of what the function does.
 - Usage: The arguments of the function and their default values.
 - Arguments: An explanation of the data each argument is expecting.
 - Details: Any important details to be aware of.
 - Value: The data the function returns.
 - See Also: Any related functions you might find useful.
 - Examples: Some examples for how to use the function.

Different functions might have different sections, but these are the main ones you should be aware of.

> ## Tip: Reading help files
>
> One of the most daunting aspects of R is the large number of functions
> available. It would be prohibitive, if not impossible to remember the
> correct usage for every function you use. Luckily, the help files
> mean you don't have to!
{: .callout}

## Special Operators

To seek help on special operators, use quotes:


~~~
?"+"
~~~
{: .r}

## Getting help on packages

Many packages come with "vignettes": tutorials and extended example documentation.
Without any arguments, `vignette()` will list all vignettes for all installed packages;
`vignette(package="package-name")` will list all available vignettes for
`package-name`, and `vignette("vignette-name")` will open the specified vignette.

If a package doesn't have any vignettes, you can usually find help by typing
`help("package-name")`.

## When you kind of remember the function

If you're not sure what package a function is in, or how it's specifically spelled you can do a fuzzy search:


~~~
??function_name
~~~
{: .r}

## When you have no idea where to begin

If you don't know what function or package you need to use
[CRAN Task Views](http://cran.at.r-project.org/web/views)
is a specially maintained list of packages grouped into
fields. This can be a good starting point.

## When your code doesn't work: seeking help from your peers

If you're having trouble using a function, 9 times out of 10,
the answers you are seeking have already been answered on
[Stack Overflow](http://stackoverflow.com/). You can search using
the `[r]` tag.

If you can't find the answer, there are a few useful functions to
help you ask a question from your peers:


~~~
?dput
~~~
{: .r}

Will dump the data you're working with into a format so that it can
be copy and pasted by anyone else into their R session.


~~~
sessionInfo()
~~~
{: .r}



~~~
R version 3.3.2 (2016-10-31)
Platform: x86_64-apple-darwin13.4.0 (64-bit)
Running under: macOS Sierra 10.12.5

locale:
[1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

attached base packages:
[1] stats     graphics  grDevices utils     datasets  base     

other attached packages:
[1] dplyr_0.5.0      ggplot2_2.2.0    checkpoint_0.4.0 stringr_1.1.0   
[5] knitr_1.14      

loaded via a namespace (and not attached):
 [1] Rcpp_0.12.7      digest_0.6.10    assertthat_0.1   R6_2.1.3        
 [5] grid_3.3.2       plyr_1.8.4       DBI_0.5          gtable_0.2.0    
 [9] formatR_1.4      magrittr_1.5     evaluate_0.9     scales_0.4.1    
[13] stringi_1.1.1    lazyeval_0.2.0   labeling_0.3     tools_3.3.2     
[17] munsell_0.4.3    colorspace_1.2-6 methods_3.3.2    tibble_1.2      
~~~
{: .output}

Will print out your current version of R, as well as any packages you
have loaded. This can be useful for others to help reproduce and debug
your issue.

## Other ports of call

* [Quick R](http://www.statmethods.net/)
* [RStudio cheat sheets](http://www.rstudio.com/resources/cheatsheets/)
* [Cookbook for R](http://www.cookbook-r.com/)
