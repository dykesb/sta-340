Activity 3 - 🎵 Your eyes are the size of the moon 🎵
================

#### Objectives

  - Identify the important features of summarizing a list of numbers.
  - Compare and contrast the shape of a set of numbers and assess the
    usefulness of shape using appropriate vocabulary.
  - Critique what kinds of summaries are best for various kinds of
    measurements.

## Overview

In Chapters 7 and 8, Utts reviews descriptive statistics and graphs for
quantitative data. In this activity, we will again make use of the
beginning of the semester survey data - your data has been combined with
data from other classes. The file you will open only contains
information on one of the questions along with class and form
information.

### The data

On the anonymous survey you (and others) completed, Question 6 asked:

Form A: Is the diameter of the moon MORE or LESS than **1,000** miles?

Form B: Is the diameter of the moon MORE or LESS than **3,000** miles?

For both forms, Question 12 then asked:

What do you think is the diameter of the mooon, in miles?

These questions were designed to elicit a specific effect.

You will need to read what Utts has to say about this effect on pages
349 – 351 of *Seeing Through Statistics*. **How do you think the answers
to Question 12 might differ based on this effect?** As part of answering
this question, you will also need to talk about what the actual diameter
of the moon is (Google to the rescue\!). As a Team you will need to
**use appropriate graphs and descriptive statistics to explore whether
this specific effect is present for Question 12**.

Write a report that address the question asked above. Your report
should:

  - Summarize the questions and the wording “trick” that you and other
    students were subjected to.
  - Act as a stand-alone document where the reader would not need to
    first read these instructions.
  - Include appropriate graphs and descriptive statistics and be sure to
    refer to the graph and statistics you include.

Prior to investigating the data, you should thoroughly discuss your
thought to the question being asked. That is, your hunch toward a *Yes*
or *No* answer to the question. Then, discuss how your graphs and
statistics either support or contradict your hunch.

Any graph or descriptive statistic that you include in your report
**must** be discussed - do not include values you do not plan to
discuss. Tables of descriptive statistics are optional, but descriptive
statistics are not.

**Post your report to your Team Google Site.** Then, provide a link to
your Google Site report for your **Team Application Task 6** submission
on Bb.

## Getting started in R

I have created an RStudio Cloud project for you at . This project has an
R script that includes code to help you:

  - Load the `tidyverse`
  - Read in the `moon.csv` data file

Code from Activity 1 and Activity 2 may help you in completing this
activity.

### A few suggestions

You will notice that scaling problem when you explore these data. I
doubt it was a serious answer, but a student gave “one billion miles”
for the diameter of the moon. A few other students gave numbers almost
as outrageously high. You should find a way to zoon in on most of the
answers, ignoring these ridiculously huge numbers. It is ok to suppress
these outlying values for visual purpose (with appropriate
acknowledgment), but be sure to compute any descriptive statistics using
the full sample.

Some hints for how to do this in R. In Activity 2, we saw that we can do
data “wrangling” (i.e., selecting/filtering data that we are interested
in investigating), then pipe (`%>%`) this into `ggplot()`. To select
rows that meet a certain critera, we can use `filter()`.

``` r
data %>% 
  filter( criteria )
```

For example, if I wanted to only look at data from Class 1, I could do:

``` r
moon_data %>% 
  filter(Class == 1)
```

If I wanted to look at data not from Class 1, I could do:

``` r
moon_data %>% 
  filter(Class != 1)
```

or, since R is recognizing Class as a numeric value,

``` r
moon_data %>% 
  filter(Class > 1)
```

or

``` r
moon_data %>% 
  filter(Class >= 2)
```

Also from Activity 2 you saw how to get summary statistics (using
`summarize()`) for different groups (using `group_by()`):

``` r
data %>% 
  group_by( grouping_variable ) %>% # You can have multiple grouping variables separated by columns
  summarize( stat = stat_function ) # We used n = n() to count
```

Various `stat_function` in R are,

  - `max(x)` – It shows the maximum value.
  - `min(x)` – Shows minimum value in a vector.
  - `mean(x)` – We obtain an arithmetic mean with this.
  - `median(x)` – Shows the median value of the vector.
  - `sd(x)` – Shows the standard deviation.
  - `mad(x)` – Shows the median absolute deviation.
  - `IQR(x)`- Shows the interquartile range.

There are missing values in the `Moon` variable so you will need to tell
R to ignore these values by doing:

``` r
function(x, na.rm = TRUE) # na.rm = TRUE informs R to ignore missing (na) values.
```

If you have questions, be sure to flag me down\!
