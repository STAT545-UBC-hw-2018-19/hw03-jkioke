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

![](hw03-jkioke_files/figure-markdown_github/unnamed-chunk-2-1.png)
