Exercise 1, Problem 3
================
elliot

=======
***Mercedes S65 AMG***
---
**Scatterplot of price against mileage**
---
>>>>>>> deaf120a7a172b07c26fb680cfb55e35a867a0d6
``` r
p_test65AMG
```

![p_test65amg](https://user-images.githubusercontent.com/47119252/52544364-24e6b100-2d76-11e9-885f-915e7dfa5331.png)


``` r
plot_grid(plot65amg.knn3, plot65amg.knn25, plot65amg.knn13, plot65amg.knn50, plot65amg.knn17, plot65amg.knn100,
          ncol = 2, axis = '1', align = 'h')
```

![grid65amg](https://user-images.githubusercontent.com/47119252/52544371-329c3680-2d76-11e9-9e03-66c97d80f273.png)

``` r
# Plot the value of model error (RMSE) vs the Number of K
plot(KnnModel65AMG, main = "Number of K vs RMSE for sclass 65AMG", xlab = "Number of K Neighbors", ylab = "RMSE (Cross-Validation)")
```

![knnmodel65amg](https://user-images.githubusercontent.com/47119252/52544386-48a9f700-2d76-11e9-83ae-565d0a08c642.png)

=======
**Optimal at k=21**
---
>>>>>>> deaf120a7a172b07c26fb680cfb55e35a867a0d6
``` r
p_test65AMG + geom_path(aes(x = mileage, y = ypred65AMG_knn21), color='red') +labs(title = "Predictive model of Price for a \n 65AMG given Mileage: KNN = 21", subtitle = "Optimal level of K")
```

![p_test65amgline](https://user-images.githubusercontent.com/47119252/52544402-5eb7b780-2d76-11e9-8d2c-0412f7cf4884.png)


=======
***Mercedes S350***
---
**Scatterplot of price against mileage**
---
>>>>>>> deaf120a7a172b07c26fb680cfb55e35a867a0d6
``` r
p_test350
```

![p_test350](https://user-images.githubusercontent.com/47119252/52544350-02ed2e80-2d76-11e9-91d0-062f81d02387.png)

``` r
plot_grid(plot350.knn3,plot350.knn10,plot350.knn20,plot350.knn40,plot350.knn60,plot350.knn80,plot350.knn100,plot350.knn120, ncol = 2, axis='1', align='h')
```

![grid65amg](https://user-images.githubusercontent.com/47119252/52544339-efda5e80-2d75-11e9-8475-0b924ffa40b4.png)

``` r
#plot RMSE vs levels of K
plot(KnnModel350, main = "Number of K vs RMSE for sclass 350", xlab = "Number of K Neighbors", ylab = "RMSE(Cross-Validation)")
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-14-1.png)

=======
**Optimal at k=13**
---
>>>>>>> deaf120a7a172b07c26fb680cfb55e35a867a0d6
``` r
p_test350 + geom_path(aes(x=mileage, y=ypred350_knn13), color='red') + labs(title ="Predictive Model of Price for a \n 350 given Mileage: Knn= 13", subtitle = "Optimal level of K")
```

![](Exercise_1,_Problem_3_files/figure-markdown_github/unnamed-chunk-16-1.png)
