Data Visualization
================
Jim Rouse
8/21/2020

This is an R Markdown document. Markdown is a simple formatting syntax
for authoring HTML, PDF, and MS Word documents. For more details on
using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

# Data Visualization

### 3.1 Introduction

``` r
# We must load the tidyverse library every session

library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------------------------------------------------------------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.1
    ## v tidyr   1.1.1     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ------------------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

### 3.2 First Steps

QUESTION: Do cars with big engines use more gas than cars with small
engines?

##### 3.2.1 mpg Data Frame

A data frame is a rectangular collection of variables (in the columns)
and observations (in the rows). mpg contains observations collected by
the US Environmental Protection Agency on 38 models of car.

### 3.2.2 Creating a ggplot

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ , y = hwy)) 
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
# The ggplot function creates a scatter plot and that is our bottom layer. The geom_point function allows for us to actually map the data that we have 
```

##### Exercises

> 1.  Run ggplot(data = mpg). What do you see?

> 2.  How many rows are in mpg? How many columns?

> 3.  What does the drv variable describe? Read the help for ?mpg to
>     find out.

> 4.  Make a scatterplot of hwy vs cyl.

> 5.  What happens if you make a scatterplot of class vs drv? Why is the
>     plot not useful?

1.  
<!-- end list -->

``` r
ggplot(data=mpg)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
\> I see just a blank coordinate grid. I think this is because we do not
have our geom\_point function to map the points within the grid.

2.  
<!-- end list -->

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l~ f        18    29 p     comp~
    ##  2 audi         a4         1.8  1999     4 manual~ f        21    29 p     comp~
    ##  3 audi         a4         2    2008     4 manual~ f        20    31 p     comp~
    ##  4 audi         a4         2    2008     4 auto(a~ f        21    30 p     comp~
    ##  5 audi         a4         2.8  1999     6 auto(l~ f        16    26 p     comp~
    ##  6 audi         a4         2.8  1999     6 manual~ f        18    26 p     comp~
    ##  7 audi         a4         3.1  2008     6 auto(a~ f        18    27 p     comp~
    ##  8 audi         a4 quat~   1.8  1999     4 manual~ 4        18    26 p     comp~
    ##  9 audi         a4 quat~   1.8  1999     4 auto(l~ 4        16    25 p     comp~
    ## 10 audi         a4 quat~   2    2008     4 manual~ 4        20    28 p     comp~
    ## # ... with 224 more rows

> There are 234 rows and 11 columns in the dataframe mpg. 3.

``` r
?mpg
```

    ## starting httpd help server ... done

> The drv variable describes the type of drive train, with f being front
> wheel drive, r being rear wheel drive, and 4 being 4 wheel drive.

4.  
<!-- end list -->

``` r
ggplot(data=mpg) + geom_point (mapping = aes (x = hwy , y = cyl))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

5.  
<!-- end list -->

``` r
ggplot(data = mpg) + geom_point (mapping = aes(x = class , y = drv ))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->
\> Answer: This plot is not useful because there seems to be no
correlation between the two, because both of the variables are
qualitative and thus we can discover nothing quantitative about the car.
However, we can discover which types of cars do not have any different
drv models.

### 3.3 Aesthetic Mappings

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ , y = hwy , color = class))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ,y = hwy , size = class))
```

    ## Warning: Using size for a discrete variable is not advised.

![](Data_Visualization_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes( x = displ , y = hwy , alpha = class))
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](Data_Visualization_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ , y = hwy , shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](Data_Visualization_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes (x = displ, y = hwy, color = class , shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](Data_Visualization_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

##### 3.3.1 Exercises

> 1.  What’s wrong with this code? Why are the points not blue?

Answer: The points are not blue because the color aesthetic needs to be
mapped to a variable, such as hwy or displ. I assume that the first
color allocation in RStudio is red, and the function created a variable
named “blue” which encompasses every point in the (x,y) dataframe.

> 2.  Which variables in mpg are categorical? Which variables are
>     continuous?

Categorical variables are: manufacturer, model, drv, class, fl,

Continuous variables are: cty, hwy, displ, year

> 3.  Map a continuous variable to color, size, and shape. How do these
>     aesthetics behave differently for categorical vs. continuous
>     variables?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy , color = cyl))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->
A continous variable cannot be mapped to shape because there are
infinitely many possible inputs because it is a number. Also, for the
color function, it turns the points into more and less transparent
points of the same color because all cars do have a cylinder, but it is
the size to which they differ that the transparency is mapping. The
graph is “continously” blue.

> 4.  What happens if you map the same variable to multiple aesthetics?

It usually maps it together, if they can correspond with one another.
Color and shape will both map concurrently.

> 5.  What does the stroke aesthetic do? What shapes does it work with?

> 6.  What happens if you map an aesthetic to something other than a
>     variable name, like aes(colour = displ \< 5)? Note, you’ll also
>     need to specify x and y.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ , y = hwy , color = displ < 5))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

### 3.5 Facets

``` r
ggplot(data = mpg) + geom_point(mapping = aes (x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ cyl)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

## 3.5 Exercises

> 1.  What happens if you facet a continouos variable?’

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ cty , nrow = 10)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->
It just produces a bunch of different small plots for all the different
quantities of city mileage. It does show how many cars have which city
mileage, but besides that it is not very helpful.

> 2.  What do the empty cells in plot with facet\_grid( drv \~ cyl)
>     represent?

They represent the fact that some combinations of the car’s drive and
it’s number of cylinders are not posessed by any car models in the
dataframe.

> 3.  What plot does the following code make? What does . do?

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->
It makes two different facet wrap functions for two different
categorical variables. I believe that the . causes one of the sections
of the facet\_grid to just be blank and hence this just makes it the
same as a facet\_wrap function as far as I know, but the categorical
variables can be plotted vertically now.

> 4.  Take the first faceted plot in this section. What are the
>     advantages to using faceting instead of color aesthetic?

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->
It allows us to more clearly seperate our data into different grids to
more clearly paint the picture of different trends between a car’s
engine displacement and highway mileage, with its type of car. It is
much more seperate and easier to decipher in this case than a color
aesthetic which would just have one big plot with a jumble of different
colors. Facets allow us to the see the subtrends of each of the
different car types.

> 5.  Read ?facet\_wrap. What does nrow do? What other options control
>     the layout of the panels? Why doesn’t facet\_grid have nrow and
>     ncol arguments?

``` r
?facet_wrap
```

It controls the number of rows of plots that will be displayed. So if
nrow = 2, then we will have two rows of subplots of the data.

> 6.  When using facet\_grid() you should usually put the variables with
>     more unique levels in the columns. Why?

Because the variable that has more unique levels will hinder the data if
plotted horizontally. In our example above, we can still see trends in
the data when we put the drv on the column but that may not be so if we
plotted it in the row.We have more space horizontally than vertically,
so whichever variables have the least number of different types should
be put on the columns.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(cyl ~ cty)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

### 3.6 Geometric Objects

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ , y = hwy , group = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = drv)) + geom_smooth(mapping = aes(x = displ, y = hwy , color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_smooth() + geom_point(mapping = aes(color = class))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

## Exercises 1-5 Only

> 1.  What geom would you use to draw a line chart? A boxplot? A
>     histogram? An area chart?

For a line chart, geom\_smooth produces a line of best fit for a given
(x,y) frame of data. For a boxplot, we have geom\_boxplot, and then
geom\_histogram, and geom\_area.

> 2.  Run this code in your head and then run it on R to check your
>     predictions about it.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->
It takes out the gray area that presents the margin of error of a line.
I think that ‘se’ stands for ‘standard error’ of the line chart, and
that is false in the code chunk above, so it does not show that area.
For everything else, the color is mapped to the ggplot() so both the
point and smooth functions have color associations.

> 3.  What does show.legend = FALSE do? What happens if you remove it?
>     Why do you think I used it earlier in the chapter?

I believe that no legend would show up on the plot. We like the legend
though because it presents us with the different associations between
lines, points with color.

> 4.  What does the se argument to geom\_smooth() do?

It represents the standard error of the geom\_smooth line function. So,
it shows us the margin of error of the line, and without it, there is no
gray area on the plot.

> 5.  Will the two graphs look different? Why/why not?

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data_Visualization_files/figure-gfm/unnamed-chunk-31-2.png)<!-- -->

No, they look the same, it is just different appearances in the code
chunk. For one, the ggplot() function globally maps the dataframe for
the geom\_point functions, and for the other, ggplot() is left blank and
the data has to be mapped to each geom individually. I think that the
top one is smoother because it does not repeat the code over again.

### 3.7 Statistical Transformations

``` r
?diamonds
```

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

``` r
?geom_bar
```

### 3.8 Position Adjustments

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = cut))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = clarity))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(alpha = 0.2, position = "Identity")
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, color = clarity)) + geom_bar(fill = NA, position = "identity")
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(position = "fill")
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(position = "dodge")
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ , y = hwy)) + geom_point(alpha = 0.3)
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point(position = "jitter")
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

##### 3.8.1 Exercises

Notebook Check - Checking for all the exercises and the notes.

Project starting next week, and due the week after

> 1.  

``` r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-43-1.png)<!-- -->
A: The problem with this plot is that all the points line up too
perfectly and this plot does not actually have every datapoint on the
graph. The data is “too tidy”

> 2.  What parameters to geom\_jitter() control the amount of jittering?

``` r
?geom_jitter
```

A: The “width” of the jitter controls the amount of jittering.

> 3.  Compare and contrast geom\_jitter() with geom\_count()

``` r
?geom_count
```

A: geom\_count will actually count the number of overlapping points and
display the numerical value of each point to the viewer, whereas
geom\_jitter will show all of the points by jittering them next to each
other.

> 4.  What is the default position adjustment for geom\_boxplot()?
>     Create a visualization of the mpg dataset that represents it?

``` r
ggplot(data = mpg) + geom_boxplot(mapping = aes(x = hwy))
```

![](Data_Visualization_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

A: The default position adjustment for geom\_boxplot is
position\_dodge().
