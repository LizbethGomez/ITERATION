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

    ##  [1]  1.04895448  0.55653396  0.57525680  0.80900339 -1.41013612
    ##  [6] -0.84895457  0.86276408 -1.45310426  0.35064018  0.16969020
    ## [11] -0.30855012  1.12753158  1.59833260 -0.79700326 -0.45361587
    ## [16] -0.13468738 -1.66518672  0.96751484 -1.92163448 -0.97499095
    ## [21] -0.03444274 -1.10414328 -0.28761990  0.84499661 -1.19773764
    ## [26]  0.40894443  1.60133207  0.14773128  0.31907710  1.20350370

``` r
(x_again- mean(x_again))/ sd(x_again)
```

    ##  [1]  0.19528965 -0.04738786 -0.23685622  1.71694310 -0.29552332
    ##  [6]  1.02161045 -0.33086607  0.02332382 -0.74913382 -1.66637107
    ## [11]  0.47620710 -0.27372558  1.17730972  0.09363654  0.99429287
    ## [16] -1.74348023  0.14079220  1.35177411 -0.38645698 -0.63489393
    ## [21] -0.99964705  1.26128154  0.87445145 -0.47423541  1.10002836
    ## [26]  1.03890197 -1.72560821 -1.85476965  0.67085630 -0.71774377

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

ˆ

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
