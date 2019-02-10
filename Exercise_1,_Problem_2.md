Exercise 1, Problem 2
================
Elliot
2/10/2019

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

``` r
# Load the 'flights' dataset and 'airports' dataset
flights <- read.csv("http://datasets.flowingdata.com/tuts/maparcs/flights.csv", header=TRUE, as.is=TRUE)
airports <- read.csv("http://datasets.flowingdata.com/tuts/maparcs/airports.csv", header=TRUE)

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

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-2-2.png)

``` r
# Graph Mean Delay for flights to Austin
ggplot(AusToAD, aes(x = Origin, y = ArrDelayMean, label = ArrDelayMean)) +
  geom_bar(stat = 'identity', aes(fill = ArrDelayMean, x = reorder(Origin, ArrDelayMean)), width = .8) +
  coord_flip() +
  scale_fill_gradient(low="green", high="red") +
  theme(text = element_text(size=10)) +
  labs(title = "Average Flight Delay for Flights into AUS") 
```

    ## Warning: Removed 1 rows containing missing values (position_stack).

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
# Graph Mean Departure Delay for all flights leaving Austin
ggplot(AusFromAD, aes(x = Dest, y = DepDelayMean, label = DepDelayMean)) +
  geom_bar(stat = 'identity', aes(fill = DepDelayMean, x=reorder(Dest, DepDelayMean)), width = .8) +
  coord_flip() +
  scale_fill_gradient(low="green", high="red") +
  theme(text = element_text(size=10)) +
  labs(title = "Average Flight Delay for Flights from AUS",
       x = "Destination",
       y = "Average Departure Delay",
       caption = "Source: ABIA") 
```

    ## Warning: Removed 1 rows containing missing values (position_stack).

![](Exercise_1,_Problem_2_files/figure-markdown_github/unnamed-chunk-6-1.png)
