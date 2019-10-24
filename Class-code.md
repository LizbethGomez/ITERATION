Writing Functions
================
Lizbeth Gomez
10/24/2019

Class slides at [Session 15 - Writing
functions](https://p8105.com/writing_functions.html) Some notes from the
slides: functions have: Arguments (input) body (code) return (fucntion’s
product)

Conditional execution: proper fornmating of if statements

## Getting started

writing fucntions

``` r
x= rnorm (n=30, mean =4, sd =2.3)
x_again= rnorm (n=30, mean =6, sd =.3)
y= rnorm (n=30, mean =24, sd =.3)
(x- mean(x))/ sd(x)
```

    ##  [1] -0.61204810  0.57770738  1.46559277 -0.92961184 -0.10344922
    ##  [6]  0.53640013 -1.16013134  0.74311034  2.92718825  0.03286167
    ## [11] -1.62180096 -0.51903987  0.19754712 -1.17456143 -0.37712446
    ## [16]  0.28422565 -0.50575841 -0.95533240 -0.77474163  1.10278756
    ## [21] -0.11645863 -0.14421965  0.30711444  1.06072990  0.04532174
    ## [26] -1.46271271  0.43627531 -1.19606080  0.74826723  1.18792197

``` r
(x_again- mean(x_again))/ sd(x_again)
```

    ##  [1] -0.03232770 -0.54615216  1.08944380 -1.43672801 -1.61319447
    ##  [6]  0.34856621  0.67397116 -0.55537229 -1.48423529  0.70404951
    ## [11] -0.49580397 -2.09213288  0.58118249  0.33836715  1.12390384
    ## [16]  1.44119875 -0.13895446 -0.22073871 -0.46854693  0.07077733
    ## [21]  0.12345508  0.64652237  0.42799237 -0.29182885 -0.51411763
    ## [26]  1.99138248 -0.17087740  1.67860473  0.43152148 -1.60992802

Now a fucntion: the x argument insude the fucntion even if there is an x
in the environment the x will be from the function

``` r
z_scores = function(x) {
  
  if(!is.numeric(x)) {
    stop("x should be numeric")
  } else if (length(x <3)) {
    stop("x should be longer than 3")
  }
  
  (x - mean(x)) / sd(x)
  
  
}
```

Trying out the
    function

``` r
z_scores(x=3)
```

    ## Error in z_scores(x = 3): x should be longer than 3

``` r
z_scores (x=y)
```

    ## Error in z_scores(x = y): x should be longer than 3

``` r
z_scores ("my name is liz")
```

    ## Error in z_scores("my name is liz"): x should be numeric

``` r
z_scores (x = c(TRUE, TRUE, FALSE, TRUE))
```

    ## Error in z_scores(x = c(TRUE, TRUE, FALSE, TRUE)): x should be numeric

``` r
z_scores(x= iris)
```

    ## Error in z_scores(x = iris): x should be numeric

## multiple outputs

no lists for now

``` r
mean_and_sd = function(input_x) {
  
  if (!is.numeric(input_x)) {
    stop("Argument x should be numeric")
  } else if (length(input_x) < 3) {
    stop("Cannot be computed for longer than 3")
  }
  
  mean_x = mean(input_x)
  sd_x = sd(input_x)

  list(mean = mean_x, 
       sd = sd_x)
}
```

\#multiple inputs

``` r
sim_data = tibble(
  x = rnorm(30, mean = 1, sd = 1),
  y = 2 + 3 * x + rnorm(30, 0, 1)
)
sim_data %>%  ggplot (aes(x=x, y=y)) +geom_point()
```

![](Class-code_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ls_fit = lm(y ~ x, data = sim_data)
  
beta0_hat = coef(ls_fit)[1]  # intercept
beta1_hat = coef(ls_fit)[2]  # slope
```

``` r
sim_regression = function(n, beta0, beta1) {
  
sim_data = tibble(
  x = rnorm(n, mean = 1, sd = 1),
  y = beta0 + beta1 * x + rnorm(n, 0, 1)
)

ls_fit = lm(y ~ x, data = sim_data)
tibble(
  beta0_hat = coef(ls_fit)[1],  # intercept
  beta1_hat = coef(ls_fit)[2]  # slope
)
}

sim_regression(n=3000, beta0 = 17, beta1 = -3)
```

    ## # A tibble: 1 x 2
    ##   beta0_hat beta1_hat
    ##       <dbl>     <dbl>
    ## 1      17.0     -2.98

``` r
sim_regression(n=3000, beta0 = 17, beta1 = -3) # can change some of the arguments and not others, as well as write them in oder without haveing to equal the variables
```

    ## # A tibble: 1 x 2
    ##   beta0_hat beta1_hat
    ##       <dbl>     <dbl>
    ## 1      17.0     -2.99
