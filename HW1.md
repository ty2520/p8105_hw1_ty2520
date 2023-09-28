HW1
================
Tongxi Yu
2023-09-21

``` r
#install.packages("moderndive")
```

``` r
library("moderndive")
library("ggplot2")
library("tidyverse")
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ lubridate 1.9.2     ✔ tibble    3.2.1
    ## ✔ purrr     1.0.2     ✔ tidyr     1.3.0
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

load dataset

``` r
data("early_january_weather")
```

``` r
#The dataset is about the hourly meterological data for LGA,, JFK and EWR in Janurary 2023. 
#important variables:
#origin: weather station
#year, month, day, hour: Time of recording.
#temp, dewp: Temperature and dewpoint in F.
#humid: Relative humidity.
#wind_dir, wind_speed, wind_gust: Wind direction (in degrees), speed and gust speed (in mph).
#precip: Precipitation, in inches.
#pressure: Sea level pressure in millibars.
#visib: Visibility in miles.
#time_hour: Date and hour of the recording as a POSIXct date.
nrow(early_january_weather)
```

    ## [1] 358

``` r
ncol(early_january_weather)
```

    ## [1] 15

``` r
mean(early_january_weather$temp)
```

    ## [1] 39.58212

making scatterplot

``` r
p1 <- ggplot(early_january_weather, aes(x = time_hour, y = temp)) + geom_point(aes(color=humid))
p1
```

![](HW1_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ggsave("temp_scatter.png")
```

    ## Saving 7 x 5 in image

``` r
set.seed(100)
x <- rnorm(10)
x
```

    ##  [1] -0.50219235  0.13153117 -0.07891709  0.88678481  0.11697127  0.31863009
    ##  [7] -0.58179068  0.71453271 -0.82525943 -0.35986213

``` r
whether_positive <- x > 0
char_vec <- c('a','b','c','d','e','f','g','h','i','j')
fac_vec <- factor(c("level 1","level 1", "level 1", "level 2", "level 2", "level 2", "level 3","level 3","level 3","level 1" ))
levels(fac_vec)
```

    ## [1] "level 1" "level 2" "level 3"

``` r
df <- data.frame(x, whether_positive,char_vec,fac_vec)
#df <- expand.grid(levels(fac_vec))
df
```

    ##              x whether_positive char_vec fac_vec
    ## 1  -0.50219235            FALSE        a level 1
    ## 2   0.13153117             TRUE        b level 1
    ## 3  -0.07891709            FALSE        c level 1
    ## 4   0.88678481             TRUE        d level 2
    ## 5   0.11697127             TRUE        e level 2
    ## 6   0.31863009             TRUE        f level 2
    ## 7  -0.58179068            FALSE        g level 3
    ## 8   0.71453271             TRUE        h level 3
    ## 9  -0.82525943            FALSE        i level 3
    ## 10 -0.35986213            FALSE        j level 1

``` r
# mean of a random sample of size 10 from a standard Normal distribution
df |> 
  pull(1) |>
  mean()
```

    ## [1] -0.01795716

``` r
# mean of a logical vector indicating whether elements of the sample are greater than 0
df |>
  pull(2) |>
  mean()
```

    ## [1] 0.5

``` r
# mean of a character vector of length 10
df |>
  pull(3) |>
  mean()
```

    ## Warning in mean.default(pull(df, 3)): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
# mean of a factor vector of length 10, with 3 different factor “levels”
df |>
  pull(-1) |>
  mean()
```

    ## Warning in mean.default(pull(df, -1)): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

mean of the random sample of size 10 and the mean of logical vector
worked but the mean of a character vector and a factor vector did not
work.

``` r
df |> 
  pull(1) |>
  as.numeric()
```

    ##  [1] -0.50219235  0.13153117 -0.07891709  0.88678481  0.11697127  0.31863009
    ##  [7] -0.58179068  0.71453271 -0.82525943 -0.35986213

``` r
df |> 
  pull(2) |>
  as.numeric()
```

    ##  [1] 0 1 0 1 1 1 0 1 0 0

``` r
df |> 
  pull(3) |>
  as.numeric()
```

    ## Warning: NAs introduced by coercion

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
df |> 
  pull(-1) |>
  as.numeric()
```

    ##  [1] 1 1 1 2 2 2 3 3 3 1

Character values wasn’t successfully transformed to numerical value so
it’s mean cannot be calculated. The mean() function needs to take in
numeric or logical values.
