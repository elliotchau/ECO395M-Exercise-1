Exercise 1, Problem 3
================
Hana Krijestorac, David Garrett, and Elliot Chau

***Mercedes S65 AMG***
---
**Scatterplot of price against mileage**
---
``` r
p_test65AMG
```

![p_test65amg](https://user-images.githubusercontent.com/47119252/52544364-24e6b100-2d76-11e9-885f-915e7dfa5331.png)

**Several models at different k-levels**
---
``` r
plot_grid(plot65amg.knn3, plot65amg.knn25, plot65amg.knn13, plot65amg.knn50, plot65amg.knn17, plot65amg.knn100,
          ncol = 2, axis = '1', align = 'h')
```

![grid65amg](https://user-images.githubusercontent.com/47119252/52544371-329c3680-2d76-11e9-9e03-66c97d80f273.png)

**Determine optimal k at lowest point**
---
``` r
# Plot the value of model error (RMSE) vs the Number of K
plot(KnnModel65AMG, main = "Number of K vs RMSE for sclass 65AMG", xlab = "Number of K Neighbors", ylab = "RMSE (Cross-Validation)")
```

![knnmodel65amg](https://user-images.githubusercontent.com/47119252/52544386-48a9f700-2d76-11e9-83ae-565d0a08c642.png)

**Optimal at k=21**
---
``` r
p_test65AMG + geom_path(aes(x = mileage, y = ypred65AMG_knn21), color='red') +labs(title = "Predictive model of Price for a \n 65AMG given Mileage: KNN = 21", subtitle = "Optimal level of K")
```

![p_test65amgline](https://user-images.githubusercontent.com/47119252/52544402-5eb7b780-2d76-11e9-8d2c-0412f7cf4884.png)


***Mercedes S350***
---
**Scatterplot of price against mileage**
---
``` r
p_test350
```

![p_test350](https://user-images.githubusercontent.com/47119252/52544472-a3dbe980-2d76-11e9-9f09-43bdf297c539.png)

**Several models at different k-levels**
---
``` r
plot_grid(plot350.knn3,plot350.knn10,plot350.knn20,plot350.knn40,plot350.knn60,plot350.knn80,plot350.knn100,plot350.knn120, ncol = 2, axis='1', align='h')
```

![grid350](https://user-images.githubusercontent.com/47119252/52544478-acccbb00-2d76-11e9-9661-8bcd5cb9790c.png)

**Determine optimal k at lowest point**
---
``` r
#plot RMSE vs levels of K
plot(KnnModel350, main = "Number of K vs RMSE for sclass 350", xlab = "Number of K Neighbors", ylab = "RMSE(Cross-Validation)")
```

![knn350](https://user-images.githubusercontent.com/47119252/52544490-c0782180-2d76-11e9-8bdb-729097e8f7ed.png)


**Optimal at k=13**
---
``` r
p_test350 + geom_path(aes(x=mileage, y=ypred350_knn13), color='red') + labs(title ="Predictive Model of Price for a \n 350 given Mileage: Knn= 13", subtitle = "Optimal level of K")
```

![knn350line](https://user-images.githubusercontent.com/47119252/52544498-cbcb4d00-2d76-11e9-9c28-aff1e7fe2048.png)

