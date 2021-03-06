Activity 1 - Getting Started with Data Visualization in R
================

#### Objectives

  - Build graphs layer-by-layer
  - Recreate graphs you (possibly) discussed in STA 215 using the
    `ggplot2` package in R
  - Describe patterns and relationships within data

## Overview

Hans Rosling was an extremely engaging public speaker and spent much of
his later years focusing on worldwide healthcare. He and his son and
daughter-in-law co-founded the Gapminder Foundation to convert
international statistics into interactive graphics to help visualize
world development
([wikipedia](https://en.wikipedia.org/wiki/Hans_Rosling#Trendalyzer_and_Gapminder)).

We will take the (approximately) four minutes to watch his [200
Counties, 4 Minutes - The Joy of Stats](https://youtu.be/jbkSRLYSojo)
BBC clip.

1.  What do you notice? What are the key take aways from this
    presentation?
2.  What do you wonder?
3.  How many variables were being showing in this visualization? What
    were they?

Take a minute to explore these data in your Teams at the
Gapminder(<https://www.gapminder.org/tools/#$chart-type=bubbles>)
website. There are a lot of slick features with this tool, but just
stick to the “Bubbles” (default) view for now.

**STOP**

#### Getting Started in R

  - Open RStudio Cloud:
      - Join our **STA340-01-W2020**
        (<https://rstudio.cloud/spaces/46200/join?access_code=DIcKuO0XmZzMNQQ0IeUHrMgkHPbSBYmDcpt7LQ8a>)
        Workspace on RStudio Cloud
      - You will be asked to log-in
      - Verify that you can see a Project called
        `activity01-data-viz-intro` and click on it to open your RStudio
        session

The amazing [Jenny Bryan](https://jennybryan.org/) packaged an excerpt
of the data available at gapminder.org of five year increments from 1952
to 2007. We will be using these data to do our best at emmulating Hans.

## The Data

  - In the **Console** (lower-left-hand pane of RStudio), type the
    following code (including the `?`)

<!-- end list -->

``` r
?gapminder::gapminder
```

  - Press **Enter**
  - Read the information that diplays in the **Help** pane
    (lower-right-hand pane of RStudio).

<!-- end list -->

4.  How many observations are in this dataset?
5.  How many variables are in this dataset? What are they?

<!-- end list -->

  - Look at the first few (first 10) observations of the `gapminder`
    dataset by typing the following code in the **Console**

<!-- end list -->

``` r
gapminder
```

  - Press **Enter**

Not the prettiest looking dataset (where are the cell dividers\!?\!),
but there is still a lot of information shown here.

*For those that are interested*: I have already pre-installed some
packages that we will be using in this activity. One of these is the
`gapminder` package. The `?` tells R that we want to find the R
Documentation for a to-be-specified package, function, or dataset. Then,
`gapminder::gapminder` tells R to look in the `gapminder` package (first
`gapminder`) for the `gapminder` object (second `gapminder`) - not the
best naming scheme.

**STOP**

-----

Before we recreate Hans’ video, we will explore:

  - scatterplots,
  - stripplots,
  - boxplots, and
  - histograms.

While producing these visualizations, we will also look at controlling
plot themes and colors. This activity is based on Jenny’s [`ggplot2`
tutorials](https://github.com/jennybc/ggplot2-tutorial).

## Scatterplots

We will start with a canvas.

  - In your `activity01.R` R script (upper-left-hand pane), type the
    following code

<!-- end list -->

``` r
p <- ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))
p
```

  - Using your mouse, highlight both lines then press **Ctrl** and
    **Enter** together on your keyboard
  - Verify that you get an image similar to…

![](activity01-data-viz-intro_files/figure-gfm/gapminder-canvas-1.png)<!-- -->

A lot to unpack here, but some of this should be familiar to you from
your Class Prep. Looking at the `ggplot(...)` portion, we are telling
the graphing tool what `data` we are using, along with what we are using
as our `x` and `y` variables.

The `p <-` portion is telling R to store/save this canvas to an object
called `p`. This allows us to build up a graph piece-by-piece without
fear of messing something up. Finally, the second line, `p`, simply
tells R to display whatever is stored in `p`. In future activities, we
will explore other things that we can assign to objects, but for now we
will stick to graphs.

**NOTE:** Whenever we add new code to an R script and we want to see
what it does, we can highlight it and **Ctrl** and **Enter** together on
out keyboard. From here on out, I will refer to this as “include and
run”.

Now, let’s *add* some “ink” to our canvas.

Scatterplots need some points, and `ggplot` uses `geom_point()` to add
points to a graphic.

  - *Below* your previous R code, include and run this additional code.

<!-- end list -->

``` r
p + geom_point()
```

6.  How would you describe this relationship?

*Below* your previous R code, include and run this additional code.

``` r
p + geom_point() + scale_x_log10()
```

7.  Compare this to your previous graph (notice the navigation arrows in
    the **Plots** pane). Which do you prefer? What does this second
    portion of code do?

Regardless of your preference, we will move forward with this
transformed x axis. Let’s make this stick - *Below* your previous R
code, include and run this code.

``` r
p <- p + scale_x_log10()
```

8.  What is `p` now?

### Scatterplot Challenge

*Below* your previous R code and using your stored `p` object,
`geom_point()`, and the `color` mapping option of `aes()` within your
geom, reproduce this plot:

![](activity01-data-viz-intro_files/figure-gfm/scatterplot-challenge-1.png)<!-- -->

**STOP**

-----

### Overplotting, part 1

One issue that occurs when there are a large number of data points (n =
1,704\!) in a data visualizations is that it is difficult to see
clustering. To address this, we can set a level of transparency and size
to the points.

  - *Below* your previous R code, include and run this additional code.

<!-- end list -->

``` r
p + geom_point(alpha = (1/3), size = 3)
```

9.  What do you notice?

10. Explore what setting different values of `alpha` and `size` do.

Later this semester we will look into time-series/line plots as well as
fitting regression lines to scatterplots.

**STOP**

-----

## Stripplots

You may have seen dotplots in STA 215. Stripplots are a way to view
dotplots for multiple groups.

11. *Below* your previous R code, create a new object, called `s`, that
    is the *canvas* for a plot to explore the relationship between `x =
    continent` and `y = lifeExp` of the `data = gapminder`.

12. *Below* your previous R code, *add* a `geom_point()` layer to `s`.
    Commment on what you notice.

### Overplotting, part 2

We previously saw that `alpha` and `size` can help address when there
are too many points to get a clear sense of what is going on in the
data. In this section, we will explore randomly jittering the points.

  - *Below* your previous R code, include and run this additional code.

<!-- end list -->

``` r
s + geom_jitter()
```

A better way to view this might be to do the following.

``` r
s + geom_jitter(position = position_jitter(width = 0.1, height = 0), alpha = (1/3))
```

![](activity01-data-viz-intro_files/figure-gfm/stripplot-1.png)<!-- -->

13. Notice that `position_jitter()` was instructed not to provide any
    vertical jitter (i.e., `height = 0`). Why do you think I chose to do
    this?

**STOP**

-----

## Boxplots

15. Boxplots are constucted using five (5) statistics. What are the
    names of these values?

16. Using your `s` object (the canvas to explore the relationship
    between `contient` and `lifeExp` of the `gapminder` data), *add* the
    boxplot geometry layer (`geom_boxplot()`).

17. Which continent has the most variability? Which continent has the
    least? What feature of the boxplot did you use to decide on this?

18. Which continent has the longest life expectancy? Which has the
    shortest life expectancy? What feature of the boxplot did you use to
    decide on this?

19. For Africa, approximately what percent of contries within Africa
    have a life expectancy longer than about 55 years?

**STOP**

-----

### Boxplots AND stripplots

20. Copy and paste your code for your first stripplot at the *bottom* of
    your R script, then *add* the boxplot geometry layer to this figure.
    Neat\!

21. Include the following argument *within* your boxplot geometry layer.
    Explore additional *named colors* using this document
    (<http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf>).

<!-- end list -->

``` r
outlier.color = "hotpink"
```

**STOP**

-----

## Histograms

22. *Below* your previous R code, create a new object, called `h`, that
    is the *canvas* for a plot to explore the distribution of `x =
    gdpPercap` of the `data = gapminder`.

23. *Below* your previous R code, *add* a `geom_histogram()` layer to
    `h`. Commment on what you notice.

24. Copy and paste your code for (23) to the *bottom* of your R script,
    then include the following argument *within* your `geom_histogram()`
    layer. Also, explore different values.

<!-- end list -->

``` r
binwidth = 1
```

25. Copy and paste your code for (23) to the *bottom* of your R script,
    then update your canvas by *add*ing the following code. What do you
    notice?

<!-- end list -->

``` r
aes(fill = continent)
```

26. Copy and paste your code for (25) to the *bottom* of your R script,
    then include the following argument *within* your `geom_histogram()`
    layer. What do you notice?

<!-- end list -->

``` r
position = "identity"
```

**STOP**

-----

### Histogram challenge

Density plots are a form or smoothed histograms. Using your `h` canvas,
the `geom_density()` layer, and the work we’ve done this far, recreate
the following plot.

![](activity01-data-viz-intro_files/figure-gfm/histogram-challenge-1.png)<!-- -->

**STOP**

-----

## Challenge

Change your theme using the examples provided at the ggplot2
documentation site
(<https://ggplot2.tidyverse.org/reference/ggtheme.html#examples>)
