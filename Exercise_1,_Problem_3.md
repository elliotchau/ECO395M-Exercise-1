Exercise 1, Problem 3
================
David Garrett, Hana Krijestorac, and Elliot Chau

**Mercedes S65 AMG**
**Scatterplot of price against mileage**
``` r
# Create base graph for plotting the testing data frame
p_test65AMG = ggplot(data = D_test65AMG) + 
  geom_point(mapping = aes(x = mileage, y = price)) +
  theme_economist()

p_test65AMG
```

![p_test65amg](https://user-images.githubusercontent.com/47119252/52541403-328e3d80-2d5a-11e9-843b-5081175cae22.png)

``` r
plot_grid(plot65amg.knn3, plot65amg.knn25, plot65amg.knn13, plot65amg.knn50, plot65amg.knn17, plot65amg.knn100,
          ncol = 2, axis = '1', align = 'h')
```

![gridknn](https://user-images.githubusercontent.com/47119252/52541496-5f8f2000-2d5b-11e9-8b11-13f68f3a84dc.png)

``` r
# Plot the value of model error (RMSE) vs the Number of K
plot(KnnModel65AMG, 
     main = "Number of K vs RMSE for sclass 65AMG", 
     xlab = "Number of K Neighbors", 
     ylab = "RMSE (Cross-Validation)")
```

![knnmodel65amg](https://user-images.githubusercontent.com/47119252/52541517-b3016e00-2d5b-11e9-9c83-afb0d36b0edd.png)

``` r
p_test65AMG + geom_path(aes(x = mileage, y = ypred65AMG_knn21), color='red') +
  labs(title = "Predictive model of Price for a \n 65AMG given Mileage: KNN = 21", 
       subtitle = "Optimal level of K")
```

![p_test65amg](https://user-images.githubusercontent.com/47119252/52541532-e7752a00-2d5b-11e9-9f5d-91d5c8caad3f.png)

``` r
#create plot
p_test350=ggplot(data=D_test350)+
  geom_point(mapping=aes(x=mileage, y=price))+
  theme_economist()

p_test350
```

![p_test350](https://user-images.githubusercontent.com/47119252/52541587-65393580-2d5c-11e9-966f-7fdcadd2657d.png)

``` r
plot_grid(plot350.knn3,plot350.knn10,plot350.knn20,plot350.knn40,plot350.knn60,plot350.knn80,plot350.knn100,plot350.knn120,
          ncol = 2, axis='1', align='h')
```

![grid350](https://user-images.githubusercontent.com/47119252/52541599-987bc480-2d5c-11e9-8c9a-213922277f60.png)

``` r
#plot RMSE vs levels of K
plot(KnnModel350, 
     main = "Number of K vs RMSE for sclass 350",
     xlab = "Number of K Neighbors",
     ylab = "RMSE(Cross-Validation)")
```

![knn350](https://user-images.githubusercontent.com/47119252/52543005-4f7f3c80-2d6b-11e9-81ee-36404136e07e.png)

``` r
p_test350 + geom_path(aes(x=mileage, y=ypred350_knn13), color='red')+
  labs(title ="Predictive Model of Price for a \n 350 given Mileage: Knn= 13",
       subtitle = "Optimal level of K")
```

![knn350line](https://user-images.githubusercontent.com/47119252/52543017-72115580-2d6b-11e9-9f17-233e9be4ee94.png)
