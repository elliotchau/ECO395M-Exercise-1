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

**Flight Delays**
-----------------

**Heading into Austin**

``` r
IntoAustin
```

![intoaustin](https://user-images.githubusercontent.com/47119252/52543868-a63c4480-2d72-11e9-9ad4-b8b8ed72a179.png)

**Heading out of Austin**

``` r
OutOfAustin
```

![outofaustin](https://user-images.githubusercontent.com/47119252/52543895-e0a5e180-2d72-11e9-90ff-2dfccf1bc9c7.png)


