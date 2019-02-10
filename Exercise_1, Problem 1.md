Exercise 1, Problem 1
================
Hana, David, and Elliot

**Density plot of all buildings**
---------------------------------

``` r
#density plots
dg = density(y[g])
plot(dg, xlab = "$/sq ft", main = "Density plot of rents for green and non-green apartments", ylim=c(0,.05), col = 'green')

dn = density(y[n])
lines(dn)

labels = c('Green', 'Non-green')
legend('topright', labels, col = c("green","black"), lty = c(1,1))
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-2-1.png)

**Low occupancy buildings removed**
-----------------------------------

``` r
#density plots
dg = density(y[g])

plot(dg, xlab = "$/sq ft", main = "Density plot of rents for green and non-green apartments", ylim=c(0,.05), col = 'green')

dn = density(y[n])
lines(dn)

labels = c('Green', 'Non-green')
legend('topright', labels, col = c("green","black"), lty = c(1,1))
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
res = cor(newdata)
View(res)

res2 = cbind(res[,5], res[,14])
colnames(res2) = c("rent", "green")
View(res2)
```

These two plots look nearly identical.

**Various correlation plots between rent and a characteristic**
---------------------------------------------------------------

``` r
#try: age
age = newdata$age
rent = newdata$Rent
plot(rent ~ age, cex = 0.5)

abline(lm(rent~age), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
#try class_a
class_a = newdata$age
rent = newdata$Rent
plot(rent ~ class_a, cex = 0.5)

abline(lm(rent~class_a), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-5-2.png)

``` r
#try amenities 
amenities = newdata$amenities
rent = newdata$Rent
plot(rent~amenities, cex = 0.5)

abline(lm(rent~amenities), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-5-3.png)

``` r
#amenities is a categorical variable so this plot wasn't useful maybe try finding mean/median

#try leasing rate
leasing_rate = newdata$leasing_rate
rent = newdata$Rent
plot(rent~leasing_rate, cex = 0.5)
abline(lm(rent~amenities), lwd = 2, col = "red")
```

![](Exercise_1_files/figure-markdown_github/unnamed-chunk-5-4.png)

``` r
#this showed a positive relationship but not the most convincing plot
```
