Exercise 1
===============
-By Hana Krijestorac, David Garrett, and Elliot Chau

Problem 1
================
The data guru's analysis was too simple. In essence, they simply assummed that several things that were not quite realistic. They are as follows:

    (1) They assumed a 100% occupancy rate.
    (2) They lumped together all buildings, old and new, and made a comparison from there.
    (3) These two assumptions resulted in an overvaluation of the green premium per square foot for rent.

First, truncating the data by removing buildings with lease rates of less than 10% is too generous. We elected to only remove buildings with zero occupancy. Second, to fairly compare green and non-green buildings, we determined that the oldest green building was 19 years old. We then removed all non-green buildings older than 19 years old. This provides an opportunity for an "apples to apples" comparison.

After doing so, we generated this chart which challenges the guru's first assumption.

``` r
BAOR
```

![baor](https://user-images.githubusercontent.com/47119252/52556145-5892fc80-2db1-11e9-9088-c64d9e136c1f.png)


The first several years clearly show that occupancy rates take time to increase. Even after the initial period, occupancy rates typically hover around 90%. This signifcantly cuts into the guru's projected rate of return.

``` r
boxplot(Rent~green_rating, data=Young, main="Rent by Building Type", 
        xlab="Green Building Designation", ylab="Rent ($)",
        ylim=c(0, 90))
```

![boxplot](https://user-images.githubusercontent.com/47119252/52556231-9132d600-2db1-11e9-9abe-02b5c323db66.png)


Now that we have determined that occupancy is far from 100%, our cleaned data set indicates that the square foot premium for green buildings is much lower than what the guru stated. After our process, we found that green buildings only command a marginal $0.60/sq ft premium. This substantially increases the period required for a break-even return on investment. The following table shows the payoff over a span of 19 years.

``` r
table
```
Over the 19 year span, this table shows that the guru drastically overestimates the payoff from the green certification.
    
    ##                Payoff
    ## Our analysis  2666567
    ## Guru         13000000

The guru predicts that they will not only pay back the investment but will return a profit. Our table indicates that this is not the case. After 19 years, the green certification will only be paid off by a little more than half the initial cost. 

Problem 2
================

**Connections to Austin Bergstrom**
-----------------------------------

**All connections**

``` r
# Create base map
basemap <- map("world", regions = c("usa"), fill = T, col = "grey8", bg = "grey15", ylim = c(21.0,50.0), xlim = c(-130.0,-65.0), main = "Map of all Airports in the Continental US")

# Overlay US airports
airportoverlay <- points(usairports$lon, usairports$lat, pch = 3, cex = 0.1, col = "chocolate1")

# Add flights connected from AUS to all other US airports
for (i in (1:dim(usairports)[1])) { 
  inter <- gcIntermediate(c(aus$lon[1], aus$lat[1]), c(usairports$lon[i], usairports$lat[i]), n=200)
  lines(inter, lwd=0.1, col="turquoise2")    
}
```

![unnamed-chunk-2-1](https://user-images.githubusercontent.com/47119252/52543816-4c3b7f00-2d72-11e9-8166-5b65b141af7b.png)

Based on this illustration, it is easy to see that Austin services many cities around the country and even several countries. 


**Direct flight connections**

``` r
# Create new map with direct flights to and from AUS
map("world", regions = c("usa"), fill = T, col = "grey8", bg = "grey15", ylim = c(21.0,50.0), xlim = c(-130.0,-65.0), main = "Map of all Direct Flights to and from Austin")
points(usairports$lon, usairports$lat, pch = 3, cex = 0.1, col = "chocolate1")

# Filter out all flights outside of the Continental US that are not directly connected to Austin
fsub <- flights[flights$airport1 == "AUS",]
for (j in 1:length(fsub$airport1)) {
  air1 <- airports[airports$iata == fsub[j,]$airport1,]
  air2 <- airports[airports$iata == fsub[j,]$airport2,]
  inter <- gcIntermediate(c(air1[1,]$long, air1[1,]$lat), c(air2[1,]$long, air2[1,]$lat), n=100, addStartEnd=TRUE)
  lines(inter, col="turquoise2", lwd=0.3)
}
```

![unnamed-chunk-1-2](https://user-images.githubusercontent.com/47119252/52543823-59f10480-2d72-11e9-9444-84afaa3db77f.png)

This graphic illustrates several domestic destinations that Austin Bergstrom directly connects with. Common with most mid-sized airports, these nonstop connections are almost exclusive with major cities that serve as frequent domestic destinations.

**Flight Delays**
-----------------

**Heading into Austin**

``` r
IntoAustin
```

![intoaustin](https://user-images.githubusercontent.com/47119252/52543868-a63c4480-2d72-11e9-9ad4-b8b8ed72a179.png)

For flights heading into Austin, San Antonio International Airport (SAT), McGhee Tyson Airport (TYS), and Birmigham-Shuttlesworth International Airport (BHM) were the top origins with the highest delays. It is difficult to pinpoint a common characteristic that would explain why those locations had longer delays other than the fact that they are medium to small sized airports in terms of traffic. 

**Heading out of Austin**

``` r
OutOfAustin
```

![outofaustin](https://user-images.githubusercontent.com/47119252/52543895-e0a5e180-2d72-11e9-90ff-2dfccf1bc9c7.png)

For traffic heading out of Austin, the top three most delayed destinations are Norfolk International Airport (ORF), Des Moines International Airport (DSM), and Newark Liberty International Airport (EWR). Again, it is difficult to find an obvious reason why this might be the case. One common characteristic is that they are all relatively far away.

Overall, average flight delays are much lower when leaving Austin than arriving. This is likely due to the fact that Austin is a destination "end point" and not a "transfer hub" for East-West (e.g. Chicago) or North-South (e.g. DC) domestic traffic.

Problem 3
================

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

**Determine optimal k at lowest RMSE**
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

**Determine optimal k at lowest RMSE**
---
``` r
#plot RMSE vs levels of K
plot(KnnModel350, main = "Number of K vs RMSE for sclass 350", xlab = "Number of K Neighbors", ylab = "RMSE(Cross-Validation)")
```

![knn350](https://user-images.githubusercontent.com/47119252/52544490-c0782180-2d76-11e9-8bdb-729097e8f7ed.png)


**Optimal at k=15**
---
``` r
p_test350 + geom_path(aes(x=mileage, y=ypred350_knn15), color='red') + labs(title ="Predictive Model of Price for a \n 350 given Mileage: Knn= 15", subtitle = "Optimal level of K")
```

![knn350line](https://user-images.githubusercontent.com/47119252/52544498-cbcb4d00-2d76-11e9-9c28-aff1e7fe2048.png)

**Which trim yields a larger optimal value of K? Why do you think this is?**
---
The S65 AMG has an optimal k=21, and the S350 has an optimal k=15. This is likely due to the sample size for the trims. Because there are more S350's in the data set (due its relatively lower price), the trim can "pull" fewer nearby data points to make an inference. It does not need to reach out as far to aid in the prediction.
