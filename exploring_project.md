exploring
================
NAME
DATE

``` r
library(readr)
LHK <- read_csv("C:/Users/Jim/Downloads/LHK.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   id = col_double(),
    ##   name = col_character(),
    ##   host_id = col_double(),
    ##   host_name = col_character(),
    ##   neighbourhood_group = col_logical(),
    ##   neighbourhood = col_character(),
    ##   latitude = col_double(),
    ##   longitude = col_double(),
    ##   room_type = col_character(),
    ##   price = col_double(),
    ##   minimum_nights = col_double(),
    ##   number_of_reviews = col_double(),
    ##   last_review = col_date(format = ""),
    ##   reviews_per_month = col_double(),
    ##   calculated_host_listings_count = col_double(),
    ##   availability_365 = col_double()
    ## )

``` r
View(LHK)
```

Load the necessary libraries

``` r
library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------------------------------------------------------------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v dplyr   1.0.1
    ## v tibble  3.0.3     v stringr 1.4.0
    ## v tidyr   1.1.1     v forcats 0.5.0
    ## v purrr   0.3.4

    ## -- Conflicts ------------------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

Take a look inside your dataset

``` r
LHK
```

    ## # A tibble: 7,209 x 16
    ##        id name  host_id host_name neighbourhood_g~ neighbourhood latitude
    ##     <dbl> <chr>   <dbl> <chr>     <lgl>            <chr>            <dbl>
    ##  1  69074 Beau~  160139 Amy       NA               Central & We~     22.3
    ##  2  75083 SoHo~  304876 Brend     NA               Central & We~     22.3
    ##  3 103760 Cent~  304876 Brend     NA               Central & We~     22.3
    ##  4 104626 Enti~  544166 Celine    NA               Central & We~     22.3
    ##  5 132773 Fabu~  304876 Brend     NA               Central & We~     22.3
    ##  6 163664 Soho~  304876 Brend     NA               Central & We~     22.3
    ##  7 163742 Soho~  304876 Brend     NA               Central & We~     22.3
    ##  8 228510 Crea~ 1192493 Michael   NA               Yau Tsim Mong     22.3
    ##  9 248140 Brig~ 1300549 Darren    NA               Central & We~     22.3
    ## 10 274589 8 mi~ 1435069 Shanshan  NA               Wan Chai          22.3
    ## # ... with 7,199 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

### Variation

Perform an analysis of the variation in the “neighbourhood” column.

``` r
ggplot(data = LHK) + 
  geom_bar(mapping = aes(x = neighbourhood)) + 
  coord_flip()
```

![](exploring_project_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

  - Which values are the most common? Why? The Yau Tsim Mong
    neighborhood has the most listings on AirBNB. This is because this
    neighbourhood is actually the biggest in Hong Kong.

  - Which values are rare? Why? Does that match your expectations? There
    are a lot of neighbourhoods with relatively very few listings,
    however this is not unusual because the \# of airBNB listings is
    mostly proportional to the population of the neighbourhood in Hong
    Kong.

  - Can you see any unusual patterns? What might explain them? No. 

Perform an analysis of the variation in the “room\_type” column.

``` r
ggplot(data = LHK) + geom_bar(mapping = aes(x = room_type, color = neighbourhood))
```

![](exploring_project_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

  - Which values are the most common? Why? The most common value here is
    the private room “room\_type”. This is because of Hong Kong’s very
    urban setting.

  - Which values are rare? Why? Does that match your expectations? The
    hotel room value is very rare, and this does match my expectations
    because I would assume that most hotels want to list their rooms
    seperately/

  - Can you see any unusual patterns? What might explain them? I think
    that an unexpected trend was for the private room to have the most
    listings but I think this is due to the distinct environment of Hong
    Kong and how many skyscrapers there are with little land on the
    island.

Perform an analysis of the variation in the “price” column. Make sure to
explore different “binwidth” values in your analysis.

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = price), binwidth = 150)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = price), binwidth = 100)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = price), binwidth = 200)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-6-3.png)<!-- -->

  - Which values are the most common? Why? A value around \~$400 a night
    seems to be the most common, however it is hard to visualize due to
    extreme outliers (I am pretty sure these outliers are not mistakes
    though, just very expensive AirBNB rentals)

  - Which values are rare? Why? Does that match your expectations? I
    would expect Hong Kong prices to be a little bit above average, but
    I bet that the price depends on the room\_type variable as private
    rooms are bound to be less expensive than whole apartments or
    houses.

  - Can you see any unusual patterns? What might explain them? There are
    many outliers to the right, and one is ever visible upwards of 80k.
    This might be real or it could be fake, but there are also many
    others upwards of 10,000. I think this can be explained by the sheer
    price/sqft of properties in the middle of Hong Kong. For the
    properties listed as a whole house/apartment, if they have alot of
    square footage they will sell for a fortune on AirBNB.

Perform an analysis of the variation in the “minimum\_nights” column.
Make sure to explore different “binwidth” values in your analysis.

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = minimum_nights), binwidth = 1)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = minimum_nights), binwidth = 5)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = minimum_nights), binwidth = 30)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-7-3.png)<!-- -->

  - Which values are the most common? Why? The value that is clearly the
    most common is simply one night. Every value between 1-7(AKA one
    week) is very commmon as well. This is because the sellers on AirBNB
    do not want to have to burden the customers with staying in a rental
    for too long, because this will dissuade many prospective buyers.

  - Which values are rare? Why? Does that match your expectations? The
    rare values are basically any value over one month. This matches my
    expectations because people want to be able to rent their property
    to the largest audience possible and there are probably less people
    looking the longer the time interval is. This histogram shows what
    is called a “right-skewed” distribution in statistics.

  - Can you see any unusual patterns? What might explain them? I do not
    see any unusual patterns in this histogram. I feel as if most of
    this was to be expected.

Perform an analysis of the variation in the “number\_of\_reviews”
column. Make sure to explore different “binwidth” values in your
analysis.

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = number_of_reviews),binwidth = 1)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = number_of_reviews),binwidth = 10)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-8-2.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = number_of_reviews),binwidth = 50)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-8-3.png)<!-- -->

  - Which values are the most common? Why? It looks as if the most
    common number of reviews is between zero and one. This is because
    AirBNB’s business appeals to first time renters who may not have
    experience renting out a home before.

  - Which values are rare? Why? Does that match your expectations? Any
    number of reviews over about 75 seems pretty rare to me, however
    there are still a good amount of homes with this many reviews. This
    “right-skewed” distribution was to be expected due to the fact
    that AirBNB really appeals to the low-scale renter, while also
    providing a platform for someone to rent out their property hundreds
    of times and receive a lot of reviews.

  - Can you see any unusual patterns? What might explain them? Nothing
    unusual.

Perform an analysis of the variation in the “availability\_365” column.
Make sure to explore different “binwidth” values in your analysis.

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = availability_365), binwidth = 1)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = availability_365), binwidth = 5) 
```

![](exploring_project_files/figure-gfm/unnamed-chunk-9-2.png)<!-- -->

``` r
ggplot(data = LHK) + 
  geom_histogram(mapping = aes(x = availability_365), binwidth = 10)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

  - Which values are the most common? Why? The most common value is 365,
    because this signals that this rental property is available for the
    whole year, which is pretty common because Hong Kong is not too
    seasonal of a destination.

  - Which values are rare? Why? Does that match your expectations? There
    are not really any “rare” values here so to speak, because I feel
    that the values 1-364 all seem roughly equally likely (with the
    exception of the two humps)

  - Can you see any unusual patterns? What might explain them? I think
    it is unusual to see a quadmodal (4 humps) histogram distribution,
    but I think that it can be explained using the seasonal context of
    AirBNB.

Questions (Part 2) Q1: What seems to be the most common name (of a
person) in the city you selected?

``` r
count(LHK, host_name) %>% 
  arrange(desc(n))
```

    ## # A tibble: 1,497 x 2
    ##    host_name          n
    ##    <chr>          <int>
    ##  1 Jovee            387
    ##  2 Jov              340
    ##  3 Ivy              292
    ##  4 Fiona            146
    ##  5 Ego              130
    ##  6 Steven           127
    ##  7 Janis            113
    ##  8 Tane Residence   107
    ##  9 Rj                79
    ## 10 Sam               74
    ## # ... with 1,487 more rows

Answer: The most common name of a person on AirBNB hosting in Hong Kong
is Jovee.

Q2: Do the number of reviews affect the price of the AirBNB? How? Why do
you think this is?

``` r
LHK_filter <- filter(LHK, price < 2000)
ggplot(data = LHK_filter) +
  geom_point(mapping = aes(x = number_of_reviews, y = price)) + 
  geom_smooth(mapping = aes(x = number_of_reviews, y = price))  
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

![](exploring_project_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

Answer: There is really no effect of number of reviews on price of
AirBNBs in Hong Kong. I think this is because there are many other
factors in Hong Kong AirBNBs that matter a lot more.

Q3: What type of room tends to have the highest AirBNB price?

``` r
ggplot(data = LHK_filter) + 
  geom_histogram(mapping = aes(x = price, fill = room_type), binwidth = 50)
```

![](exploring_project_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->
Answer: the entire home/apartment room type tends to have the highest
AirBNB price.

Q4: What neighborhoods tend to have the highest AirBNB price

``` r
ggplot(data = LHK_filter) + 
  geom_boxplot(mapping = aes(x = neighbourhood, y = price)) + 
  coord_flip()
```

![](exploring_project_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->
Answer: The Kwai Tsing neighborhood of Hong Kong has the highest median
AirBNB price

Q5: Suppose you could purchase a property in the city you selected, and
that you could rent it to others as an AirBNB. In what neighborhood
would you purchase your property? Why?

``` r
#want to calculate the difference between the property prices and median AirBNB price in the neighborhood; Do some research 
```

Answer: I would purchase a home in the Southern neighborhood because
from the period 2010-2019, home prices were steadily increasing and
outpacing the rest of Hong Kong, which can be expected to continue.

Part 3

``` r
LHK_by_neighborhood <- LHK %>% 
  group_by(neighbourhood) 

LHK_by_neighborhood
```

    ## # A tibble: 7,209 x 16
    ## # Groups:   neighbourhood [18]
    ##        id name  host_id host_name neighbourhood_g~ neighbourhood latitude
    ##     <dbl> <chr>   <dbl> <chr>     <lgl>            <chr>            <dbl>
    ##  1  69074 Beau~  160139 Amy       NA               Central & We~     22.3
    ##  2  75083 SoHo~  304876 Brend     NA               Central & We~     22.3
    ##  3 103760 Cent~  304876 Brend     NA               Central & We~     22.3
    ##  4 104626 Enti~  544166 Celine    NA               Central & We~     22.3
    ##  5 132773 Fabu~  304876 Brend     NA               Central & We~     22.3
    ##  6 163664 Soho~  304876 Brend     NA               Central & We~     22.3
    ##  7 163742 Soho~  304876 Brend     NA               Central & We~     22.3
    ##  8 228510 Crea~ 1192493 Michael   NA               Yau Tsim Mong     22.3
    ##  9 248140 Brig~ 1300549 Darren    NA               Central & We~     22.3
    ## 10 274589 8 mi~ 1435069 Shanshan  NA               Wan Chai          22.3
    ## # ... with 7,199 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

Use your dataset to find what the average price/night is in the
neighborhood you selected

``` r
ggplot(data = LHK_filter) + 
  geom_boxplot(mapping = aes(x = neighbourhood, y = price)) + 
  coord_flip()
```

![](exploring_project_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->
Answer: The average price per night in my neighbourhood(Southern) is
about 750 dollars per night.

Use your dataset to find what the average number of available nights per
year is in the neighborhood you selected.

``` r
ggplot(data = LHK_filter) + 
  geom_boxplot(mapping = aes(x = neighbourhood, y = availability_365)) + 
  coord_flip()
```

![](exploring_project_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->
Answer: the average number of available nights in the Southern
neighborhood is about 260 nights.

### Calculations of break even price

It will take approximately 7 years to break even on AirBNB using the
average number of nights available and \~700 dollars per night (my
property is a little bit below average in the neighborhood at only 1.2
million dollars). In conclusion, Hong Kong’s Southern neighborhood is
not the best place to try to build an AirBNB business. This is because
Hong Kong is already dominated by the condo market that buying homes is
so expensive.

``` r
7*700*260
```

    ## [1] 1274000

(ALL DOLLAR VALUES ARE USD)
