Conducting Correlations in R
================
Israel Arevalo
2023-01-22

- <a href="#data-preparation" id="toc-data-preparation">Data
  Preparation</a>
- <a href="#conducting-correlations"
  id="toc-conducting-correlations">Conducting Correlations</a>
- <a href="#visualizing-the-results"
  id="toc-visualizing-the-results">Visualizing the Results</a>

Correlation is a statistical measure that can be used to determine the
strength and direction of the relationship between two variables. In R,
the `cor()` function can be used to calculate correlation coefficients.
In this tutorial, we will use simulated educational data to demonstrate
how to conduct correlations in R.

As in previous guides, several assumptions about the user will be made.

1.  You have installed R and an IDE such as RStudio on your computer
2.  You have a dataset to work with (we will generate a dataset in this
    tutorial but you will need a dataset to run your own analysis
    outside of the tutorial, of course)

For additional information, please follow the links below as necessary.

- [Installing
  RStudio](https://rstudio-education.github.io/hopr/starting.html)
- [Exporting SPSS dataset to
  .CSV](https://www.ibm.com/docs/en/spss-statistics/beta?topic=files-exporting-datasets)
- [Exporting STATA dataset to
  .csv](https://stats.oarc.ucla.edu/stata/faq/how-do-i-export-stata-dta-files-to-comma-separated-files/)
- [Exporting Excel file to
  .csv](https://support.microsoft.com/en-us/office/import-or-export-text-txt-or-csv-files-5250ac4c-663c-47ce-937b-339e391393ba)

# Data Preparation

First, we will need to load in the necessary packages and create the
simulated data set. For this tutorial, we will create a data set that
contains information on students’ math scores and reading scores.

``` r
# Loading Packages
library(ggplot2)
```

``` r
set.seed(123)  # for reproducibility

# create the data set
data <- data.frame(student_id = 1:30,
                   math_score = rnorm(30, mean = 70, sd = 10),
                   reading_score = rnorm(30, mean = 75, sd = 12))
```

Next, we will take a look at the structure of the data set using the
`str()` function.

``` r
str(data)
```

    ## 'data.frame':    30 obs. of  3 variables:
    ##  $ student_id   : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ math_score   : num  64.4 67.7 85.6 70.7 71.3 ...
    ##  $ reading_score: num  80.1 71.5 85.7 85.5 84.9 ...

# Conducting Correlations

Now that we have the data loaded, we can calculate the correlation
coefficient between the `math_score` and `reading_score` variables. The
`cor.test()` function can be used to calculate the Pearson’s correlation
coefficient, which is the most commonly used correlation coefficient.

``` r
cor.test(data$math_score, data$reading_score)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data$math_score and data$reading_score
    ## t = -0.84368, df = 28, p-value = 0.406
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.4899292  0.2150148
    ## sample estimates:
    ##        cor 
    ## -0.1574511

The correlation coefficient output, `-0.1574511`, is a number between -1
and 1 that indicates the strength and direction of the relationship
between the two variables, in this case `math_score` and
`reading_score`.

A positive coefficient indicates a positive correlation, meaning that as
one variable increases, the other variable also tends to increase. A
negative coefficient indicates a negative correlation, meaning that as
one variable increases, the other variable tends to decrease. A
coefficient of 0 indicates no correlation.

In this case, the correlation coefficient is negative, which suggests
that there is a small negative correlation between the `math_score` and
`reading_score` variables. This means that as math scores increase,
reading scores tend to decrease slightly. The correlation coefficient of
`-0.1574511` is quite close to 0, which indicates that the relationship
between the two variables is weak. This means that although there is a
weak negative correlation between math scores and reading scores, it is
not very strong.

In order to test whether the correlation coefficient obtained is
statistically significant, we can use a hypothesis test. The null
hypothesis is that there is no correlation between the two variables,
and the alternative hypothesis is that there is a correlation.

The test statistic used to test the significance of the correlation
coefficient is the t-value. The t-value is calculated by dividing the
correlation coefficient by its standard error. The standard error of the
correlation coefficient is calculated using a specific formula that
takes into account the sample size, the standard deviation of the two
variables and the correlation coefficient.

To test the significance of the correlation coefficient, we use the
t-value to calculate a p-value. The p-value represents the probability
of observing a t-value as large or larger than the one computed from the
data, assuming that the null hypothesis is true. A low p-value
(typically less than 0.05) indicates that the correlation coefficient is
statistically significant, and the null hypothesis can be rejected.

We can see these values available on our table output. The t-value is a
measure of how different the correlation coefficient is from zero. The
larger the t-value, the more evidence we have that there is a
correlation between the two variables. The t-value in this case is
`-0.84368`.

The next value is the p-value, which represents the probability of
observing a t-value as large or larger than the one computed from the
data, assuming that the null hypothesis is true. The p-value in this
case is `0.406` which is greater than 0.05 (commonly used significance
level). Therefore, we fail to reject the null hypothesis that there is
no correlation between the two variables.

The last value is the confidence interval, which is a range of values
that is likely to contain the true correlation coefficient. The 95%
confidence interval in this case is between `-0.4899292` and
`0.2150148`. This means that if we were to conduct this test multiple
times, 95% of the time the true correlation coefficient would fall
within this range.

# Visualizing the Results

Finally, we can create a scatter plot to visualize the relationship
between the two variables.

``` r
ggplot(data, aes(x = math_score, y = reading_score)) +
  geom_smooth(method = "lm", color = "red") +
  ggtitle("Scatter plot of Math Scores vs Reading Scores")
```

![](correlations_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

This plot shows the relationship between the `math_score` and
`reading_score` variables, and can help to further illustrate the
strength and direction of the correlation. The line of best fit (in red)
shows the direction of the correlation and the slope of the line
represents the strength of the correlation.

In summary, this tutorial demonstrated how to conduct a correlation
analysis using simulated educational data in R. The steps outlined in
this tutorial can be applied to any data set and any set of variables.
Correlation analysis is a useful tool for identifying the relationship
between two variables, and it can provide insights into the extent to
which two variables are related. Additionally, visualizing the results
using the `ggplot2` package can help to further understand the
relationship between the variables.

Please keep in mind that correlation does not imply causation, just
because two variables are correlated does not mean that one variable
causes the other. It’s important to consider other factors that may be
impacting the relationship between the variables.
