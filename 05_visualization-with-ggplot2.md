Visualization
================
2026-10-06

# Visualization and EDA

This is visualization

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(p8105.datasets)
```

``` r
library(p8105.datasets)
data("weather_df")
```

Now we have everything we need! Start with a scatter plot
你可以使用設定，在圖的表現上，完整呈現你希望展示的東西

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) + 
  labs(
    title = "Temperature (Max vs Min)",
    x = "Max Temperature (C)",
    y = "Min Temperature (C)",
    color="Location",
    caption = "Data from NOAA for three weather stations package"
  )
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](05_visualization-with-ggplot2_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

let’s try some other scales
當你使用label的時候，你可以改變label,圖片對應的label會改變
你也可以把圖片上的位置進行相應的調整和改變

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) + 
  labs(
    title = "Temperature (Max vs Min)",
    x = "Max Temperature (C)",
    y = "Min Temperature (C)",
    color="Location",
    caption = "Data from NOAA for three weather stations package"
  )+ 
  scale_x_continuous(
    breaks = c(-15, 0, 15),
    labels = c("-15º C", "0", "Fifteen")+
      scale_y_continuous(
    trans = "sqrt", 
    position = "right")
  )
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](05_visualization-with-ggplot2_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

Lets look at color!
當你不喜歡圖片的顏色的時候，你可以自己改圖片的顏色，用一些設定，去進行相應的改變
scale_color_hue可以用來改變color的scale（？）

``` r
weather_df |> 
  ggplot(aes(x = tmax, y = tmin,color=name)) + 
  geom_point() + 
  scale_color_hue(h = c(100, 300))
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](05_visualization-with-ggplot2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

當你覺得改顏色不方便的時候，可以用viridis這個package

``` r
weather_df |> 
  ggplot(aes(x = tmax, y = tmin,color=name)) + 
  geom_point() + 
  viridis::scale_color_viridis(
    name = "Location", 
    discrete = TRUE
  )
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](05_visualization-with-ggplot2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->
