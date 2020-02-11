Activity 2 - How moral are we?
================

#### Objectives

  - Build graphs layer-by-layer
  - Recreate graphs you (possibly) discussed in STA 215 using the
    `ggplot2` package in R
  - Describe patterns and relationships within data

## Overview

One of the topics covered in STA 215 here at GVSU is the *Chi-Square
Test of Independence*. This test can be used to determine whether or not
there is evidence that two qualitative variables are related. In this
activity I will help you in performing a Chi-Square test in R, but you
and your team members will be responsible for writing a document that
interweaves narrative, answers to some specific questions, and
statistical output.

In Section 3.2 *It’s All in the Wording* Utts gives examples and
discusses the drastic effect wording of survey questions can have on the
results. In this activity, we will consider another example using data
already collected from you.

At the end of this activity, students will be able to: - Summarize
categorical data using R - Perform a chi-square test using R - Download
graphics from R to use in reports

#### Getting started in R

  - Open RStudio Cloud (<https://rstudio.cloud/>) and enter our
    **STA340-01-W2020** class workspace.
      - You will be asked to log-in
      - Verify that you can see a Project called
        `activity02-how-moral-R-we` and click on it to open your RStudio
        session
      - In the **Files** pane (lower right-hand pane), verify that you
        have an `activity02-how-moral-R-we.R` R script and a `/data`
        folder that contains a file called `survey-wallet.csv`.
      - Double-click to open the `activity02-how-moral-R-we.R` script
        and verify that it contains the following code:

<!-- end list -->

``` r
## Load R packages
library(tidyverse)
library(infer)

## Read in data
wallet <- read_csv("data/survey-wallet.R")

...
```

We will continue working with this R script.

## Prepping data for analysis

First, highlight lines 1-6 of the R script and run it (Ctrl + Enter).

Remember the anonymous survey you were asked to fill out the first day?
Unknown to you, there were two forms of the survey.

Form A: If you found a wallet with $20 in it, would you keep the money?
YES NO

Form B: If you found a wallet with $20 in it, would you do the honest
thing and return it? YES NO

I have also created a new variable named `Moral`. You and your team
members will be responsible for interpreting this variable later.

To view these data, go to the **Environment** pane (upper right-hand
pane) and click on the dataset’s name. A new tab next to your script
should open called *wallet* that looks like a spreadsheet. Explore this
for a little bit, then remember to close the tab.

For the variable `Wallet`, the values are not very informative. Let’s
change that\! For both forms of the question, 1 = YES and 2 = NO.

Under the `## Prepping data for analysis` header, add the following
code:

``` r
wallet <- wallet %>% 
  mutate(Wallet = case_when(
    Wallet == 1 ~ "YES",
    Wallet == 2 ~ "NO"
  ))
```

Check out the `wallet` dataset again. What did this code do?

In this dataset, I created a variable named `Moral`. Determine what this
variable means and label it appropriately.

## A test of independence

Say we wish to assess if the way this survey question was worded impacts
how students responded to it (I am purposefully being vague with
describing the problem here). To do these, we should first summarize our
results (both numerically and visually) to discuss what we notice and
what we wonder, then conduct the appropriate test (here, a chi-square
test of independence). Before we do this, provide detail for the
following question. You should include this in your final write up.

1.  The two wordings were meant to deliberately produce bias in the
    results. Before we do any sort of analysis of the data, give your
    best guess for how the results might be influenced by the wording.
    Give some thought to whether a YES or NO answer to each question
    indicates a “moral” response.

### Exploratory data analysis

We will now create a two-way contingency table to explore our problem.
Add the following code to your script line-by-line (with me) and we
explore what each line is doing. I will add comments in my R script that
you are more than welcome to also include in yours for reference.

``` r
wallet %>% 
  group_by(Moral, Wallet) %>% 
  summarize(n = n()) %>% 
  mutate(percent = n / sum(n) * 100) %>% 
  pivot_wider(-n, names_from = Moral, values_from = percent)
```

I will leave the interpretation of these values to your team. Now we
will create a clustered bar chart to visualize this two-way contingency
table. Add the following code to your script and we will again explore
it line-by-line.

``` r
wallet %>% 
  group_by(Moral, Wallet) %>% 
  summarize(n = n()) %>% 
  mutate(percent = n / sum(n) * 100) %>% 
  ggplot(mapping = aes(x = Moral, y = percent, fill = Wallet)) +
  geom_bar(stat = "identity", position = "dodge")
```

To save this, in the **Plots** pane (lower right-hand pane) click on the
Export. Here you can choose from some different options.

### Chi-square test

Now we will formally test our research question using a chi-square test
of independence. Add the following code to your script and we will again
explore it line-by-line.

``` r
wallet %>% 
  chisq_test(Moral ~ Wallet)
```

## Team Application Task 3

As a group, write up a report that addresses \[1\] above as well as
\[2\] and \[3\] listed below. Include an introduction that summarizes
the survey question and the wording ‘trick’ you were subjected to. It
should work as a stand-alone document; in other words, the reader would
not need to first read these instructions. You need to include and
discuss the exploratory analysis in your write-up. You do not need to
include the chi-square test results, but should discuss them. This will
be uploaded to your Teams Google Site. I expect about one page.

**Note**: We did the above steps using `Wallet` and `Moral`, but I
expect you to make use of the variables `Form` and `Moral`. You might be
interested in how this particular class responded to these survey
questions, but I expect you to analyze all of the data, lumping all the
classes together.

2.  Summarize the survey results using the most appropriate descriptive
    statistics. Discuss this in context relative to your answer for \#1.

3.  Make appropriate use of a chi-square test. Did you find a
    significant association for the population of students this sample
    represents? Discuss this in context relative to your answers for \#1
    and 2. If you need to review the chi-square test, see STS chapter
    13.
