Function\_
================
Bre
2023-11-02

# Assignment B1 - *Making a function*

I will start off by calling packages that I might need for this
assignment. I do this using the library() function.

``` r
library(dplyr)
library(tidyverse)
library(datateachr)
library(testthat)
```

## Making a function:

I decided to make a function using a combination of dplyr functions that
I have used together repeatedly. I thought that combining these into a
single function would help to streamline the coding process.

``` r
getNamesCount <- function(df, categoricalCol, numericalCol, numericalValue) {
  if (!is.numeric(numericalValue)) {
    stop("Check that your numericalValue input is a number.")
  }
  result <- df %>% 
    filter(!is.na({{ numericalCol }}), {{ numericalCol }} < numericalValue) %>% 
    select({{ categoricalCol }})
  
  count <- nrow(result)
  
  return(count)
}
```

This function can be used to count the number of categorical
observations that meet the criteria of being below a certain numerical
value taken from the numerical column.

It works well if you would like to know the number of observations you
have in your data that meet a certain numerical criteria.

#### Error Message:

In making the function I used *!is.numeric* to stop the
**getNamesCount** function from running if there is a value put in for
*‘numericalValue’* which is not a number. I also used the stop()
function prompting the **getNamesCount** function to throw up the error
message **“Check that your numericalValue input is a number.”** if the
function detects that the numericalValue input is not a number.

#### Function creation:

I chose to use the *!is.na* combined with the *curly-curly* operator to
prompt the function to look down the numerical column that it is given
and filter out NA observations. The *curly_curly* operator again is used
to look down the numerical column that it is given and filter for
observations which are less that the given numerical value (which is
from the numerical column). Then using the *curly_curly* operator once
more we look down the observations from the categorical column which
meet the numerical criteria previously filtered for. The number of
categorical column observations that match the criteria from the
numerical column are counted using *nrow()*. The count is returned as
the function answer using *return()*.

## Documenting the **getNamesCount** function - *using roxygen2*

``` r
#' Count names that fall within a numerical value range
#' 
#' The getNamesCount() function can be used to count the number of observations in a categorical column that meet the value criteria specified from a numerical column.
#'
#' @param df Data or data frame - I named this 'df' to stand for data frame. I thought that df was short and self-explanatory for this argument. 
#' @param categoricalCol A column containing categorical variables. - I named this 'categoricalCol' in a similar style to the function name with the second word being capitalized to maintain uniformity, and categorical column is a shortened form of categorical column which is what should be entered. 
#' @param numericalCol A column contain numerical values. - Similar in logic to the other names, 'numericalCol' is named to represented a numerical column. 
#' @param numericalValue A number from the numerical values column. - I chose to use the same prefix 'numerical' for both 'numericalCol' and 'numericalValue' to indicate that the number use for the numerical value should come from the numerical colunm.
#' @return This function returns a numerical output, from the row counts after filtering.
#' @examples 
#' getNamesCount(df, categoricalColName, numericalColName, 5)
#' 
getNamesCount <- function(df, categoricalCol, numericalCol, numericalValue) {
  if (!is.numeric(numericalValue)) {
    stop("Check that your numericalValue input is a number.")
  }
  result <- df %>% 
    filter(!is.na({{ numericalCol }}), {{ numericalCol }} < numericalValue) %>% 
    select({{ categoricalCol }})
  
  count <- nrow(result)
  
  return(count)
}
```

## Examples of using the **getNamesCount** function:

### Example 1:

I am looking at the data set *vancouver_trees* from the datateachr()
package and I would like to see how many observations I have for trees
with a diameter less than 7. I would use the **getNamesCount** function
to write the following code.

``` r
answer1.0 <- getNamesCount(vancouver_trees, common_name, diameter, 7)

print(answer1.0)
```

    ## [1] 60553

### Example 2:

I want to do the same count as above but I would like to narrow down the
number of trees.

``` r
answer2.0 <- getNamesCount(vancouver_trees, common_name, diameter, 1)

print(answer2.0)
```

    ## [1] 123

You can see by testing the function here there are less trees with a
diameter that is very small (at a value less than 1).

### Example 3:

Now I want to check that it knows there are no trees in existence
anywhere in Vancouver with a diameter less than 0 .

``` r
answer3.0 <- getNamesCount(vancouver_trees, neighbourhood_name, diameter, 0)

print(answer3.0)
```

    ## [1] 0

This count comes back correctly with 0 trees in Vancouver at a diameter
less than 0.

### Example 4:

I am going to use a different data set from the datateachr() package for
this example. I will use the *apt_buildings* data to check how many
buildings we have heating type data for that also have less than 20
units.

``` r
answer4.0 <- getNamesCount(apt_buildings, heating_type, no_of_units, 20)

print(answer4.0)
```

    ## [1] 654

### Showing an error using the **getNamesCount** function:

``` r
answer5.0 <- getNamesCount(vancouver_trees, neighbourhood_name, diameter, word) 
```

    ## Error in getNamesCount(vancouver_trees, neighbourhood_name, diameter, : Check that your numericalValue input is a number.

The error above demonstrates the code stopping if a number is not put in
for the argument ‘numericalValue’. Showing the error code “Check that
your numericalValue input is a number”.

## Testing the **getNamesCount()** function using the *testthat* package:

### Test that the functions output is numeric:

``` r
test_that("getNamesCount function test for numeric output", {
  output <- getNamesCount(vancouver_trees, common_name, diameter, 2)
  expect_true(is.numeric(output), info = "The function output should numeric")
})
```

    ## Test passed 🥇

### Test the error message for the *numericalValue* input:

``` r
test_that("getNamesCount function error message with non-numeric numericalValue input", {
  expect_error(getNamesCount(vancouver_trees, common_name, diameter, word),
               "Check that your numericalValue input is a number.", 
               info = "The getNamesCount function should display error message for a non-numeric numericalValue")
})
```

    ## Test passed 🥇

### Test that the function filters for NA values:

To do this I will make a simple sample data frame and call it
**dfSample**.

``` r
 dfSample <- data.frame(
    fruit = c("apple", "banana", "cherry", "coconut", "dragonfruit"),
    numFruit = c(17, NA, 35, 49, 102))

  print(dfSample)
```

    ##         fruit numFruit
    ## 1       apple       17
    ## 2      banana       NA
    ## 3      cherry       35
    ## 4     coconut       49
    ## 5 dragonfruit      102

Now I will use the testthat package to confirm that the NA observation
is not counted.

``` r
test_that("getNamesCount function test for filtering NA observations", {
  output <- getNamesCount(dfSample, fruit, numFruit, 103)
  expect_equal(output, 4, info = "getNamesCount function should filter NA observations out of count")
})
```

    ## Test passed 🎊

It worked! As the count output was 4, which mean that it counted all the
numeric variables that satisfied the argument (less that 103).
