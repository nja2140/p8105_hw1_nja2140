p8105\_hw1\_nja
================

Problem 1: create a data frame comprised of: a random sample of size 8
from a standard Normal distribution a logical vector indicating whether
elements of the sample are greater than 0 a character vector of length 8
a factor vector of length 8, with 3 different factor “levels”

Try to take the mean of each variable in your dataframe. What works and
what
    doesn’t?

``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.0       ✔ purrr   0.3.2  
    ## ✔ tibble  2.1.1       ✔ dplyr   0.8.0.1
    ## ✔ tidyr   0.8.3       ✔ stringr 1.4.0  
    ## ✔ readr   1.3.1       ✔ forcats 0.4.0

    ## ── Conflicts ───────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
set.seed(545)
problem1_df = tibble(
  norm_samp = rnorm(8),
  vec_logical = norm_samp >0,
  vec_char = c("The", "dog", "ran", "over", "the", "fence", "right", "now"),
  vec_factor = factor(c("low", "medium", "high", "low", "high", "medium", "low", "medium"))
)
mean(pull(problem1_df, norm_samp))
```

    ## [1] -0.3186373

``` r
mean(pull(problem1_df, vec_logical))
```

    ## [1] 0.5

``` r
mean(pull(problem1_df, vec_char))
```

    ## Warning in mean.default(pull(problem1_df, vec_char)): argument is not
    ## numeric or logical: returning NA

    ## [1] NA

``` r
mean(pull(problem1_df, vec_factor))
```

    ## Warning in mean.default(pull(problem1_df, vec_factor)): argument is not
    ## numeric or logical: returning NA

    ## [1] NA

``` r
results = 'hide'
as.numeric(pull(problem1_df, vec_logical))
```

    ## [1] 1 1 0 0 0 0 1 1

``` r
as.numeric(pull(problem1_df, vec_char))
```

    ## Warning: NAs introduced by coercion

    ## [1] NA NA NA NA NA NA NA NA

``` r
as.numeric(pull(problem1_df, vec_factor))
```

    ## [1] 2 3 1 2 1 3 2 3

I was able to take the mean of the first 2 variables of norm\_samp and
vec\_logical. I was not able to take the mean of the second 2 variables
of vec\_char and vec\_factor. When I run the as.numeric function on
vec\_logical, vec\_char and vec\_factor, I see results for both
vec\_logical and vec\_factor but not vec\_char. This is because the
function of as.numeric converted both the vec\_logical and vec\_factor
into a coded number. For example, for vec\_logical convereted True and
False into either 0 or 1, while for vec\_factor it converted low, medium
and high into either 1, 2 or 3. Since the variable vec\_char is a string
of random character variables, no nuemeric values are able to be added,
which is why the output is NA. This does help explain why we were not
able to take the mean above. If we now tried to take a mean of the
numeric versions of vev\_logical and vec\_factor, then we theoretically
should be able to take them.

In a second code chunk: convert the logical vector to numeric, and
multiply the random sample by the result convert the logical vector to a
factor, and multiply the random sample by the result convert the logical
vector to a factor and then convert the result to numeric, and multiply
the random sample by the result

``` r
eval = TRUE
as.numeric(pull(problem1_df, vec_logical))*(pull(problem1_df, norm_samp))
```

    ## [1] 0.4693106 0.5007676 0.0000000 0.0000000 0.0000000 0.0000000 0.6785886
    ## [8] 0.1743609

``` r
as.factor(pull(problem1_df, vec_logical))*(pull(problem1_df, norm_samp))
```

    ## Warning in Ops.factor(as.factor(pull(problem1_df, vec_logical)),
    ## (pull(problem1_df, : '*' not meaningful for factors

    ## [1] NA NA NA NA NA NA NA NA

``` r
as.numeric(as.factor(pull(problem1_df, vec_logical))*(pull(problem1_df, norm_samp)))
```

    ## Warning in Ops.factor(as.factor(pull(problem1_df, vec_logical)),
    ## (pull(problem1_df, : '*' not meaningful for factors

    ## [1] NA NA NA NA NA NA NA NA

Problem 2: Create a data frame comprised of: x: a random sample of size
500 from a standard Normal distribution y: a random sample of size 500
from a standard Normal distribution A logical vector indicating whether
x + y \> 1 A numeric vector created by coercing the above logical vector
A factor vector created by coercing the above logical vector

``` r
set.seed(1234)
problem2_df = tibble(
  x = rnorm(500),
  y = rnorm(500),
  vec_logical_2 = x + y >1,
  vec_numeric_2 = as.numeric(vec_logical_2),
  vec_factor_2 = as.factor(vec_logical_2)
)
```

Write a short description of your vector using inline R code, including:
\* the size of the dataset (using nrow and ncol) \* the mean, median,
and standard deviation of x \* the proportion of cases for which x + y
\> 1

The size of the dataset `problem2_df` is 500 rows and 5 columns

The mean of x is 0.0018388, The median is -0.0207073, The standard
deviation is 1.0348139 The proportion of cases for which x + y \>1 is
0.232

Make a scatterplot of y vs x; color points using the logical variable
(adding color = … inside of aes in your ggplot code should help). Make a
second and third scatterplot that color points using the numeric and
factor variables, respectively, and comment on the color
scales

``` r
ggplot(problem2_df) + geom_point(aes(x = x, y = y), color = 'blue') 
```

![](HW-1-R-code-_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggsave("scatter_plot.pdf", plot = last_plot())
```

    ## Saving 7 x 5 in image

``` r
ggplot(problem2_df) + geom_point(aes(x=vec_numeric_2, y=y), color = 'pink')
```

![](HW-1-R-code-_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->

``` r
ggplot(problem2_df) + geom_point(aes(x=vec_factor_2, y=y), color = 'yellow')
```

![](HW-1-R-code-_files/figure-gfm/unnamed-chunk-4-3.png)<!-- -->
