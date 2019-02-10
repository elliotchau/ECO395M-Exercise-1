PS1 Exercise 1
================
Elliot

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

``` r
#density plots
dg = density(y[g])

plot(dg, xlab = "rent per sq ft", main = "density plot of rents for green and not green apartments", ylim=c(0,.05), col = 'green')

dn = density(y[n])
lines(dn)

labels = c('green', 'non-green')
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
