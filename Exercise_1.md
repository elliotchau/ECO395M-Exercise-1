PS1 Exercise 1
================
Elliot

``` r
library (tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.5
    ## ✔ tibble  2.0.1     ✔ dplyr   0.7.8
    ## ✔ tidyr   0.8.1     ✔ stringr 1.2.0
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## Warning: package 'tibble' was built under R version 3.4.4

    ## Warning: package 'tidyr' was built under R version 3.4.4

    ## Warning: package 'purrr' was built under R version 3.4.4

    ## Warning: package 'dplyr' was built under R version 3.4.4

    ## Warning: package 'forcats' was built under R version 3.4.3

    ## ── Conflicts ───────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
greenbuildings <- read.csv("greenbuildings.csv")
y = greenbuildings$Rent
summary(y)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    2.98   19.50   25.16   28.42   34.18  250.00

``` r
yTotal = y*greenbuildings$size
summary(yTotal)
```

    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ##     19488   1161242   3276324   7284883   8910330 469243000

``` r
green = greenbuildings$green_rating

#indices of rows that are green (g) vs not green (n)
g = which(green == 1)
n = which(green == 0)

length(g)
```

    ## [1] 685

``` r
length(n)
```

    ## [1] 7209

``` r
#density plots
dg = density(y[g])
plot(dg, xlab = "$/sq ft", main = "Density plot of rents for green and non-green apartments", ylim=c(0,.05), col = 'green')

dn = density(y[n])
lines(dn)

labels = c('Green', 'Non-green')
legend('topright', labels, col = c("green","black"), lty = c(1,1))
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-1-1.png)

``` r
#remove low occupancy
low = which(greenbuildings$leasing_rate < 10)
high = which(greenbuildings$leasing_rate >= 10)

newdata = greenbuildings[high,]

green = newdata$green_rating

#indices of rows that are green (g) vs not green (n)
g = which(green == 1)
n = which(green == 0)

length(g)
```

    ## [1] 684

``` r
length(n)
```

    ## [1] 6995

``` r
y = newdata$Rent

#density plots
dg = density(y[g])

plot(dg, xlab = "rent per sq ft", main = "density plot of rents for green and not green apartments", ylim=c(0,.05), col = 'green')

dn = density(y[n])
lines(dn)

labels = c('green', 'non-green')
legend('topright', labels, col = c("green","black"), lty = c(1,1))
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-1-2.png)

``` r
res = cor(newdata)
View(res)

res2 = cbind(res[,5], res[,14])
colnames(res2) = c("rent", "green")
View(res2)

#try: age
age = newdata$age
rent = newdata$Rent
plot(rent ~ age, cex = 0.5)

abline(lm(rent~age), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-1-3.png)

``` r
#try class_a
class_a = newdata$age
rent = newdata$Rent
plot(rent ~ class_a, cex = 0.5)

abline(lm(rent~class_a), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-1-4.png)

``` r
#try amenities 
amenities = newdata$amenities
rent = newdata$Rent
plot(rent~amenities, cex = 0.5)

abline(lm(rent~amenities), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-1-5.png)

``` r
#amenities is a categorical variable so this plot wasn't useful maybe try finding mean/median

#try leasing rate
leasing_rate = newdata$leasing_rate
rent = newdata$Rent
plot(rent~leasing_rate, cex = 0.5)
abline(lm(rent~amenities), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-1-6.png)

``` r
#this showed a positive relationship but not the most convincing plot
```
