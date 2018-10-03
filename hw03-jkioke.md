hw03-gapminder
================
kioke
September 29, 2018

Tasks
=====

Pick three of the tasks and present a table and a figure for each.

### How is life expectancy changing over time on different continents?

The figure below shows life expectancy over time, separated by continent by the colour of the points.

``` r
gapminder %>% 
  ggplot(aes(year,lifeExp,colour=continent)) +
  geom_jitter(alpha=0.33) +
  labs(x = "Year", y = "Life Expectancy") #To change the axis labels
```

![](hw03-jkioke_files/figure-markdown_github/unnamed-chunk-1-1.png) We could also choose to represent the different continents on different plots by facetting the data, if the above figure is too visually busy to read.

``` r
gapminder %>% 
  ggplot(aes(year,lifeExp)) +
  geom_jitter(alpha=0.2) +
  facet_wrap( ~ continent) +
  labs(x = "Year", y = "Life Expectancy")
```

![](hw03-jkioke_files/figure-markdown_github/unnamed-chunk-2-1.png) Below is a table summarizing the above figures globally.

``` r
gapminder %>% 
  group_by(year) %>% 
  summarize(mean_life_exp = mean(lifeExp))
```

    ## # A tibble: 12 x 2
    ##     year mean_life_exp
    ##    <int>         <dbl>
    ##  1  1952          49.1
    ##  2  1957          51.5
    ##  3  1962          53.6
    ##  4  1967          55.7
    ##  5  1972          57.6
    ##  6  1977          59.6
    ##  7  1982          61.5
    ##  8  1987          63.2
    ##  9  1992          64.2
    ## 10  1997          65.0
    ## 11  2002          65.7
    ## 12  2007          67.0

We can also look at the means over time in a table with continents as another variable.

``` r
gapminder %>% 
  group_by(year,continent) %>% 
  summarize(mean_life_exp = mean(lifeExp))
```

    ## # A tibble: 60 x 3
    ## # Groups:   year [?]
    ##     year continent mean_life_exp
    ##    <int> <fct>             <dbl>
    ##  1  1952 Africa             39.1
    ##  2  1952 Americas           53.3
    ##  3  1952 Asia               46.3
    ##  4  1952 Europe             64.4
    ##  5  1952 Oceania            69.3
    ##  6  1957 Africa             41.3
    ##  7  1957 Americas           56.0
    ##  8  1957 Asia               49.3
    ##  9  1957 Europe             66.7
    ## 10  1957 Oceania            70.3
    ## # ... with 50 more rows

### Mean Life Expectancy, 1982-1997

In order to compute the mean of any data between 1982 and 1997, we first need to filter out other years

``` r
mill <- gapminder %>% 
  filter(year >= 1982 & year <= 1997)
```

Now to determine the mean life expectancy of those years.

``` r
mill %>% 
  group_by(continent) %>% 
  summarize(mean_mill_life_exp = mean(lifeExp))
```

    ## # A tibble: 5 x 2
    ##   continent mean_mill_life_exp
    ##   <fct>                  <dbl>
    ## 1 Africa                  53.0
    ## 2 Americas                68.8
    ## 3 Asia                    65.5
    ## 4 Europe                  74.1
    ## 5 Oceania                 76.2

``` r
mill %>% 
  ggplot(aes(gdpPercap, lifeExp)) +
  geom_point() + 
  scale_x_log10()
```

![](hw03-jkioke_files/figure-markdown_github/unnamed-chunk-7-1.png)

``` r
mill %>% 
  group_by(continent) %>% 
  summarize(mean_mill_life_exp = mean(lifeExp)) %>% 
  ggplot(aes(continent, mean_mill_life_exp)) +
  geom_point(size = 3) +
  labs(x = "Continent", y = "Mean Life Expectancy 1982-1997")
```

![](hw03-jkioke_files/figure-markdown_github/unnamed-chunk-8-1.png)
