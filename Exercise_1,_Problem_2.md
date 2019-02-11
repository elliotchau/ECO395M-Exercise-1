Exercise 1, Problem 2
================
David Garrett, Hana Krijestorac, and Elliot Chau

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

This graphic illustrates several domestic destinations that Austin Bergstrom directly connects with. Common with most mid-sized airports, these nonstop connections are almost exclusive with major cities that either serve as destinations or connections in that direction.

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

