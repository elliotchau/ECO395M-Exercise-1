Exercise 1, Problem 1
================

``` r
BAOR
```

![](Exercise_1,_Problem_1_files/figure-markdown_github/unnamed-chunk-2-1.png)

``` r
boxplot(Rent~green_rating, data=Young, main="Rent by Building Type", 
        xlab="Green Building Designation", ylab="Rent ($)",
        ylim=c(0, 90))
```
=======
The first several years clearly show that occupancy rates take time to increase. Even after the initial period, occupancy rates typically hover around 90%. This signifcantly cuts into the guru's projected rate of return.

=======
The first several years clearly show that occupancy rates take time to increase. Even after the initial period, occupancy rates typically hover around 90%. This signifcantly cuts into the guru's projected rate of return.

=======
The first several years clearly show that occupancy rates take time to increase. Even after the initial period, occupancy rates typically hover around 90%. This signifcantly cuts into the guru's projected rate of return.


![](Exercise_1,_Problem_1_files/figure-markdown_github/unnamed-chunk-3-1.png)

``` r
table
```

Over the 19 year span, this table shows that the guru drastically overestimates the payoff from the green certification.
    ##                Payoff
    ## Our analysis  2666567
    ## Guru         13000000
