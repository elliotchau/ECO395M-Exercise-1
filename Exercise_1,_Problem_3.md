Exercise 1, Problem 3
================
elliot

``` r
# Create base graph for plotting the testing data frame
p_test65AMG = ggplot(data = D_test65AMG) + 
  geom_point(mapping = aes(x = mileage, y = price)) +
  theme_economist()

p_test65AMG
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-2-1.png)

``` r
plot_grid(plot65amg.knn3, plot65amg.knn25, plot65amg.knn13, plot65amg.knn50, plot65amg.knn17, plot65amg.knn100,
          ncol = 2, axis = '1', align = 'h')
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
# Plot the value of model error (RMSE) vs the Number of K
plot(KnnModel65AMG, 
     main = "Number of K vs RMSE for sclass 65AMG", 
     xlab = "Number of K Neighbors", 
     ylab = "RMSE (Cross-Validation)")
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-6-1.png)

``` r
p_test65AMG + geom_path(aes(x = mileage, y = ypred65AMG_knn21), color='red') +
  labs(title = "Predictive model of Price for a \n 65AMG given Mileage: KNN = 21", 
       subtitle = "Optimal level of K")
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-8-1.png)

``` r
#create plot
p_test350=ggplot(data=D_test350)+
  geom_point(mapping=aes(x=mileage, y=price))+
  theme_economist()

p_test350
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-10-1.png)

``` r
plot_grid(plot350.knn3,plot350.knn10,plot350.knn20,plot350.knn40,plot350.knn60,plot350.knn80,plot350.knn100,plot350.knn120,
          ncol = 2, axis='1', align='h')
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-12-1.png)

``` r
#plot RMSE vs levels of K
plot(KnnModel350, 
     main = "Number of K vs RMSE for sclass 350",
     xlab = "Number of K Neighbors",
     ylab = "RMSE(Cross-Validation)")
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-14-1.png)

``` r
p_test350 + geom_path(aes(x=mileage, y=ypred350_knn13), color='red')+
  labs(title ="Predictive Model of Price for a \n 350 given Mileage: Knn= 13",
       subtitle = "Optimal level of K")
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-16-1.png)
