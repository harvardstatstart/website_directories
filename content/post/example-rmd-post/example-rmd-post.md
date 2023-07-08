---
title: "Data Visualization"
author: "Jenny lee"
date: 2024-07-08T21:13:14-05:00
categories: ["R"]
tags: ["R Markdown", "Data Visualization"]
---



# Section 1: Data Visualization

## Load R packages, data, and settings

```r
library("dslabs") # to load data(gapminder)
library("tidyverse") # to use %>%
library("ggplot2")
library("RColorBrewer")
data(gapminder)
```

## Trend plots: Legends
- Life expectancy over years for each country (e.g. South Korea and Germany).
- Tell `ggplot` to separate the two curves/lines by country.
- Use `color` argument to assign different colors to different countries.

```r
countries <- c("South Korea","Germany")
plot_legend <- gapminder %>% 
  filter(country %in% countries) %>% 
  ggplot(aes(year, life_expectancy, col = country)) +
  geom_line() +
  theme(legend.position="bottom")
plot_legend
```

<img src="/post/example-rmd-post/example-rmd-post_files/figure-html/unnamed-chunk-2-1.png" width="672" />

## Trend plots: Labeling
- Define a data table with label locations and map these labels.

```r
labels <- data.frame(country = countries, x = c(1970,1970), y = c(60,75))
plot_label <- plot_legend + 
  geom_text(data = labels, aes(x, y, label = country), size = 5) + 
  theme(legend.position = "none") 
plot_label
```

<img src="/post/example-rmd-post/example-rmd-post_files/figure-html/unnamed-chunk-3-1.png" width="672" style="display: block; margin: auto;" />

## Think of the Color Blind
- ~10% of the population is color blind. Default colors in `ggplot2` are not great.
- `RColorBrewer` has several color palettes (e.g. [color blind friendly pallet](http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/#a-colorblind-friendly-palette)).


```r
RColorBrewer::display.brewer.all(colorblindFriendly = TRUE)
```

<img src="/post/example-rmd-post/example-rmd-post_files/figure-html/unnamed-chunk-4-1.png" width="672" style="display: block; margin: auto;" />
