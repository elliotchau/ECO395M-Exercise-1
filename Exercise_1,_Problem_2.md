Exercise 1, Problem 2
================
David Garrett, Hana Krijestorac, and Elliot Chau

**Connections to Austin Bergstrom**
-----------------------------------

**All connections**

``` r
# Create base map
basemap <- map("world",
    regions = c("usa"),
    fill = T,
    col = "grey8",
    bg = "grey15",
    ylim = c(21.0,50.0),
    xlim = c(-130.0,-65.0),
    main = "Map of all Airports in the Continental US")

# Overlay US airports
airportoverlay <- points(usairports$lon,
       usairports$lat,
       pch = 3,
       cex = 0.1,
       col = "chocolate1")

# Add flights connected from AUS to all other US airports
for (i in (1:dim(usairports)[1])) { 
  inter <- gcIntermediate(c(aus$lon[1], aus$lat[1]), c(usairports$lon[i], usairports$lat[i]), n=200)
  lines(inter, lwd=0.1, col="turquoise2")    
}
```

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-2-1.png)

**Direct flight connections**

``` r
# Create new map with direct flights to and from AUS
map("world",
    regions = c("usa"),
    fill = T,
    col = "grey8",
    bg = "grey15",
    ylim = c(21.0,50.0),
    xlim = c(-130.0,-65.0),
    main = "Map of all Direct Flights to and from Austin")

points(usairports$lon,
       usairports$lat,
       pch = 3,
       cex = 0.1,
       col = "chocolate1")

# Filter out all flights outside of the Continental US that are not directly connected to Austin
fsub <- flights[flights$airport1 == "AUS",]
for (j in 1:length(fsub$airport1)) {
  air1 <- airports[airports$iata == fsub[j,]$airport1,]
  air2 <- airports[airports$iata == fsub[j,]$airport2,]
  
  inter <- gcIntermediate(c(air1[1,]$long, 
                            air1[1,]$lat), 
                          c(air2[1,]$long, 
                            air2[1,]$lat), 
                          n=100, 
                          addStartEnd=TRUE)
  
  lines(inter, 
        col="turquoise2",
        lwd=0.3)
}
```

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-4-1.png)

**Flight Delays**
-----------------

**Heading into Austin**

``` r
IntoAustin
```

    ## Warning: Removed 1 rows containing missing values (position_stack).

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-7-1.png)

**Heading out of Austin**

``` r
OutOfAustin
```

    ## Warning: Removed 1 rows containing missing values (position_stack).

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-10-1.png)
