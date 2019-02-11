Exercise 1, Problem 1
================
The data guru's analysis was too simple. In essence, they simply assummed that several things that were not quite realistic. They are as follows:

    (1) They assumed a 100% occupancy rate.
    (2) They lumped together all buildlings, old and new, and made a comparison from there.
    (3) These two assumptions resulted in an overvaluation of the green premium per square foot for rent.

First, truncating the data by removing buildlings with lease rates of less than 10% is too generous. We elected to only remove buildings with zero occupancy. Second, to fairly compare green and non-green buildlings, we determined that the oldest green buildling was 19 years old. We then removed all non-green buildlings older than 19 years old. This provides an opportunity for an "apples to apples" comparison.

After doing so, we generated this chart which challenges the guru's first assumption.

``` r
BAOR
```

![baor](https://user-images.githubusercontent.com/47119252/52553900-c5ef5f00-2daa-11e9-835e-e49cae657023.png)

The first several years clearly show that occupancy rates take time to increase. Additionally, based on this graph, green buildings so show slightly higher rates compared to non-green buildlings.

Now that we have determined that occupancy is far from 100%, our cleaned data set indicates that the square foot premium for green buildings is much lower than what the guru stated. After our process, we found that green buildings only command a $0.60/sq ft premium. This substantially increases the period required for a break-even return on investment. The following table shows the payoff over a span of 19 years.

``` r
table
```
Over the 19 year span, this table shows that the guru drastically overestimates the payoff from the green certification.
    ##                Payoff
    ## Our analysis  2666567
    ## Guru         13000000

The guru predicts that they will not only pay back the investment but will return a profit. Our table indicates that this is not the case. After 19 years, the green certification will only be paid off by a little more than half the initial cost. 
