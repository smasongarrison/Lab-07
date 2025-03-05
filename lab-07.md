Lab 07 - Conveying the right message through visualisation
================
Zi Li
3/3

### Load packages and data

``` r
library(tidyverse) 
```

### Exercise 1

``` r
# This plot oversimplified the concept of wear mask, and other situations, like quarantine policy, health baseline. 
# The original visualization somehow have dual Y-Axis Scaling, making direct comparisons difficult.
# Based on this plot, it seems like mask mandates lead to higher cases initially.


covid_data <- tribble(
  ~date, ~covid_cases, ~counties,
  "03/1/2020",  23, "Mask",
  "03/1/2020", 10.2, "No Mask",
  "03/2/2020", 19.6, "Mask",
  "03/2/2020", 10, "No Mask",
  "03/3/2020", 19, "Mask",
  "03/3/2020", 10, "No Mask",
  "03/4/2020", 19.4, "Mask",
  "03/4/2020", 9.8, "No Mask",
  "03/5/2020", 18.9, "Mask",
  "03/5/2020", 10.2, "No Mask",
  "03/6/2020", 19, "Mask",
  "03/6/2020", 9.7, "No Mask",
  "03/7/2020", 20, "Mask",
  "03/7/2020", 10, "No Mask",
  "03/8/2020", 16.3, "Mask",
  "03/8/2020", 9.7, "No Mask",
  "03/9/2020", 17, "Mask",
  "03/9/2020", 9, "No Mask",
  "03/10/2020", 17.1, "Mask",
  "03/10/2020", 9, "No Mask",
  "03/11/2020", 17.2, "Mask",
  "03/11/2020", 10, "No Mask",
  "03/12/2020", 17.3, "Mask",
  "03/12/2020", 9.6, "No Mask",
  "03/13/2020", 17.5, "Mask",
  "03/13/2020", 10, "No Mask",
  "03/14/2020", 17.4, "Mask",
  "03/14/2020", 11, "No Mask",
  "03/15/2020", 17.4, "Mask",
  "03/15/2020", 13, "No Mask",
  "03/16/2020", 17.3, "Mask",
  "03/16/2020", 14, "No Mask",
  "03/17/2020", 17, "Mask",
  "03/17/2020", 16, "No Mask",
  "03/18/2020", 16.7, "Mask",
  "03/18/2020", 16.7, "No Mask",
  "03/19/2020", 16, "Mask",
  "03/19/2020", 17, "No Mask",
  "03/20/2020", 15.5, "Mask",
  "03/20/2020", 20, "No Mask"
)
covid_data
```

    ## # A tibble: 40 × 3
    ##    date      covid_cases counties
    ##    <chr>           <dbl> <chr>   
    ##  1 03/1/2020        23   Mask    
    ##  2 03/1/2020        10.2 No Mask 
    ##  3 03/2/2020        19.6 Mask    
    ##  4 03/2/2020        10   No Mask 
    ##  5 03/3/2020        19   Mask    
    ##  6 03/3/2020        10   No Mask 
    ##  7 03/4/2020        19.4 Mask    
    ##  8 03/4/2020         9.8 No Mask 
    ##  9 03/5/2020        18.9 Mask    
    ## 10 03/5/2020        10.2 No Mask 
    ## # ℹ 30 more rows

``` r
# 3 columns, and 31 rows; this dataset shows an increase in mask-wearing and a decrease in COVID-19 cases-in general- over time.
```

### Exercise 2

``` r
covid_data <- covid_data %>%
  mutate(date = as.Date(date, format = "%m/%d/%Y"))
 
ggplot(covid_data, aes(x = date, y = covid_cases, color = counties, group = counties)) +
  geom_line(size = 1) +  
  scale_color_manual(values = c("Mask" = "lightblue", "No Mask" = "pink")) +  
  labs( title = "COVID-19 Cases Over Time in Mask vs. No Mask Counties",
    x = "Date",
    y = "COVID-19 Cases Per 100K Population",
    color = "County Type"
  )
```

    ## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
    ## ℹ Please use `linewidth` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

![](lab-07_files/figure-gfm/accurately%20visualization-1.png)<!-- -->

``` r
# my plot show a clear decrease trend for mask wearing; and a increase trend for no mask counties. and we can clearly see how wearing mask vs. not wearing mask affect covid cases. 
# and my plot labeled mask vs no mask with different color, it's more clear than the original plot. 
```

``` r
# What, if any, useful information do these data and your visualization tell us about mask wearing and COVID? It’ll be difficult to set aside what you already know about mask wearing, but you should try to focus only on what this visualization tells. Feel free to also comment on whether that lines up with what you know about mask wearing.

# so only based on my visualization, it seems like wearing mask reduces the rate of covid, but it takes time to see this effect; whereas without a mask, the effect is less pronounced initially, but as time goes on, the rate of covid increases. 
# And while wearing a mask will slow down the chances of getting the covid, it's not a complete elimination. There are still cases of covid in both masked and non-masked areas.
```

``` r
# the easier way would be change the Y-axis to make it seems like the cases increased in mask-wearing counties.
# and change the color, to attract the attention. 


ggplot(covid_data, aes(x = date, y = covid_cases, color = counties, group = counties)) +
  geom_line(size = 1.2) +
  scale_color_manual(values = c("Mask" = "pink", "No Mask" = "blue")) +  
  scale_y_reverse() + 
  labs( title = "COVID-19 Cases Over Time in Mask vs. No Mask Counties",
    subtitle = "just kidding",
    x = "Date",
    y = "COVID-19 Cases Per 100K Population",
    color = "County Type"
  )
```

![](lab-07_files/figure-gfm/misleading%20visz-1.png)<!-- -->

``` r
# Discuss the key factors that contribute to this message, such as the variables used, the scale of the axes, and the type of visualization.

# the variables we have are the: date (X-axis), which allowing a clear view of trends over time; and covid_cases (Y-axis) which is the measure of the infection rate; and counties shows the COVID-19 cases per 100K population, which is the primary measure of infection rate; and counties (colored as "Mask" Vs. "No Mask") given a easy comparison between two groups.

# I use a Line Graph, because this graph shows trends over time.

# In my opposite visualization, I flipped the Y-axis to make it look like the COVID cases in counties without masks were progressively decreasing. The misleading message I was trying to convey was that the masks had no effect and even increased COVID-19 cases.
```

Add exercise headings as needed.
