Lab 02 - Plastic waste
================
Natalie Frye
2/7/21

## Load packages and data

``` r
library(tidyverse) 
```

``` r
plastic_waste <- read_csv("data/plastic-waste.csv")
```

## Exercises

### Exercise 1

The continents seems to be fairly similar in their plastic waste per
capita. North America has one or two outliers of countries with much
higher high plastic waste per capita.

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2) +
  facet_wrap(~ continent)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_bin).

![](lab-02_files/figure-gfm/plastic-waste-continent-1.png)<!-- -->

### Exercise 2

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap, 
                     color = continent, 
                     fill = continent)) +
  geom_density(alpha = .2)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_density).

![](lab-02_files/figure-gfm/plastic-waste-density-1.png)<!-- -->

### Exercise 3

Color and fill are defined using the aesthetics of the plot because we
wanted them to be based on the value of variables in the dataset,
whereas we wanted alpha to just be a property of the plot and not
determined by the data, so we made it a characteristic of the plotting
geom.

### Exercise 4

Remove this text, and add your answer for Exercise 4 here.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = continent, 
                     y = plastic_waste_per_cap)) +
  geom_violin()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_ydensity).

![](lab-02_files/figure-gfm/plastic-waste-violin-1.png)<!-- -->

The violin plots allow you to see the density plot, which isn’t in a
regular box plot. The median and upper and lower quartiles of each
distribution are more readily apparent in a regular box plot, since they
are marked with distinct lines.

### Exercise 5

There seems to be a slightly positive linear relationship between
mismanaged plastic waste per capita and plastic waste per capita.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = mismanaged_plastic_waste_per_cap, 
                     y = plastic_waste_per_cap)) +
  geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-1.png)<!-- -->

### Exercise 6

Europe and North America seems to have a stronger relationship between
plastic waste and mismanaged plastic waste, while Africa seems to have a
weaker relationship between the two.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = mismanaged_plastic_waste_per_cap, 
                     y = plastic_waste_per_cap, color = continent)) +
  geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-continent-1.png)<!-- -->

### Exercise 7

I wouldn’t really say either variable looks more strongly linearly
associated with plastic waste. Maybe the coastal population is slightly
more so.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = total_pop, 
                     y = plastic_waste_per_cap, color = continent)) +
  geom_point()
```

    ## Warning: Removed 61 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-population-total-1.png)<!-- -->

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = coastal_pop, 
                     y = plastic_waste_per_cap, color = continent)) +
  geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-population-coastal-1.png)<!-- -->

### Exercise 8

Remove this text, and add your answer for Exercise 8 here.

``` r
plastic_waste_filtered <- filter(plastic_waste, plastic_waste_per_cap < 3)
ggplot(data = plastic_waste_filtered,
       mapping = aes(x = coastal_pop / total_pop, 
                     y = plastic_waste_per_cap)) +
  geom_point(mapping = aes(color = continent)) +
  geom_smooth(color = "#000000") + 
scale_color_viridis_d() +
  labs(title = "Plastic waste vs. coastal population proportion",
       subtitle = "by continent",
       x = "coastal population proportion (Coastal/total population)", y = "Plastic waste per capita")
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 10 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 10 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/recreate-viz-1.png)<!-- -->
