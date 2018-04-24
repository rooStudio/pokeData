PokéData
================

Purpose
-------

The purpose of this document is to showcase the ability of R to extract data from websites, and to showcase said data in some funky visualisations!

Including Code
--------------

Firstly, we need to build a function which allows us to extract specific elements of a website. We can do this by using the rvest package.

``` r
getNode <- function(url, xpath){
  # Fetch the rvest library. If it doesn't exist on this env. then install first!
  if (!require('rvest')) install.packages('rvest'); library('rvest')
  # Fetch html content (wrapped in a trycatch to mitigate 404)
  tryCatch(
    content <-
      paste(read_html(url) %>% html_nodes(xpath = xpath) %>% html_text(), collapse = ' '),
    error = function(e) {
      NA
    }
  )
  return(content)
}
```

This results in the following

``` r
x <- getNode('https://www.theguardian.com','//*[@id="headlines"]/div/div[2]/div[1]/ul/li[1]/div/div/a')
```

    ## Loading required package: rvest

    ## Loading required package: xml2

``` r
print(x)
```

    ## [1] "Tech firms could face new EU regulations over fake news"

Including Plots
---------------

You can also embed plots, for example:

![](test_github_files/figure-markdown_github/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
