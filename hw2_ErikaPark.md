Homework 2
================
Erika Park
9/28/2021

``` r
library(dplyr)
library(nycflights13)
```

#### 1\. How many flights have a missing dep\_time? What other variables are missing? What might these rows represent?

#### 2\. Currently dep\_time and sched\_dep\_time are convenient to look at, but hard to compute with because they’re not really continuous numbers. Convert them to a more convenient representation of number of minutes since midnight.

``` r
flights %>% select(dep_time, sched_dep_time)
```

    ## # A tibble: 336,776 × 2
    ##    dep_time sched_dep_time
    ##       <int>          <int>
    ##  1      517            515
    ##  2      533            529
    ##  3      542            540
    ##  4      544            545
    ##  5      554            600
    ##  6      554            558
    ##  7      555            600
    ##  8      557            600
    ##  9      557            600
    ## 10      558            600
    ## # … with 336,766 more rows

``` r
flights %>% 
  mutate(dep_minutes_since_midnight = (dep_time %/% 100)* 60 + (dep_time %%100),
         sched_minutes_since_midnight = (sched_dep_time %/% 100) * 60 + (sched_dep_time %% 100)) #%>% View
```

    ## # A tibble: 336,776 × 21
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 336,766 more rows, and 13 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>,
    ## #   dep_minutes_since_midnight <dbl>, sched_minutes_since_midnight <dbl>

#### 3\. Look at the number of canceled flights per day. Is there a pattern? Is the proportion of canceled flights related to the average delay? Use multiple dyplr operations, all on one line, concluding with ggplot(aes(x= ,y=)) + geom\_point()
