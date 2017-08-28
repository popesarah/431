Working with Data in R
================
Thomas E. Love
2017-08-27

-   [What is this?](#what-is-this)
-   [Getting Started](#getting-started)
-   [Editing the R Markdown file](#editing-the-r-markdown-file)
-   [Loading in a Data Set](#loading-in-a-data-set)
-   [Chunks of R Code](#chunks-of-r-code)
    -   [Chunk Options](#chunk-options)
    -   [Chunks of Code, Interspersed with Text](#chunks-of-code-interspersed-with-text)
-   [Basic Numerical Summaries](#basic-numerical-summaries)
    -   [On Rounding](#on-rounding)
    -   [Using Other Packages](#using-other-packages)
-   [Functions from Dr. Love](#functions-from-dr.-love)
    -   [skew1](#skew1)
    -   [Emp\_Rule: Does the 68-95-99.7 "Empirical Rule" Work Well for these Data?](#emp_rule-does-the-68-95-99.7-empirical-rule-work-well-for-these-data)
-   [Assessing Correlations](#assessing-correlations)
    -   [Pearson Correlations](#pearson-correlations)
    -   [Spearman Correlations](#spearman-correlations)
-   [Plotting a Single Batch of Data](#plotting-a-single-batch-of-data)
    -   [Histogram](#histogram)
    -   [Frequency Polygon](#frequency-polygon)
    -   [Density Plot](#density-plot)
    -   [Comparing a Histogram to a Normal Model](#comparing-a-histogram-to-a-normal-model)
    -   [Boxplot for a Single Batch of Data](#boxplot-for-a-single-batch-of-data)
    -   [Stem and Leaf Display](#stem-and-leaf-display)
    -   [Dot Plot](#dot-plot)
-   [Building Plots to Assess Normality and Transformations](#building-plots-to-assess-normality-and-transformations)
    -   [Normal Q-Q Plot (using the ggplot2 library)](#normal-q-q-plot-using-the-ggplot2-library)
    -   [Normal Q-Q Plot (without the ggplot2 library)](#normal-q-q-plot-without-the-ggplot2-library)
-   [Plotting Multiple Plots in the Same Figure](#plotting-multiple-plots-in-the-same-figure)
    -   [Plotting Nine Plots in the Same Figure (Ladder of Power Transformations)](#plotting-nine-plots-in-the-same-figure-ladder-of-power-transformations)
-   [Plotting a Quantitative Outcome and a Categorical Predictor](#plotting-a-quantitative-outcome-and-a-categorical-predictor)
    -   [Comparison Boxplot with Notches](#comparison-boxplot-with-notches)
    -   [Using a Violin Plot to Compare Distributions](#using-a-violin-plot-to-compare-distributions)
    -   [Comparing Distributions with Faceted Histograms](#comparing-distributions-with-faceted-histograms)
    -   [Faceted Density Plots](#faceted-density-plots)
    -   [Joy Plot](#joy-plot)
-   [Plotting a Quantitative Outcome and a Quantitative Predictor](#plotting-a-quantitative-outcome-and-a-quantitative-predictor)
    -   [Scatterplot with loess smooth](#scatterplot-with-loess-smooth)
    -   [Scatterplot with linear fit](#scatterplot-with-linear-fit)
-   [Fitting a Linear Model to Describe the Association](#fitting-a-linear-model-to-describe-the-association)
    -   [Making Predictions](#making-predictions)
-   [Adding in a Categorical Predictor](#adding-in-a-categorical-predictor)
    -   [Scatterplots faceted by a Categorical Predictor](#scatterplots-faceted-by-a-categorical-predictor)
    -   [Scatterplots showing Multiple Categories at once](#scatterplots-showing-multiple-categories-at-once)
-   [Fitting a Linear Model to account for one Quantitative Predictor, one Categorical Predictor and their Interaction](#fitting-a-linear-model-to-account-for-one-quantitative-predictor-one-categorical-predictor-and-their-interaction)
    -   [Making Predictions using Model 2](#making-predictions-using-model-2)
-   [Plotting the Association of Multiple Variables](#plotting-the-association-of-multiple-variables)
    -   [A Scatterplot Matrix (GGally approach)](#a-scatterplot-matrix-ggally-approach)
    -   [Plotting a Correlation Matrix (GGally approach)](#plotting-a-correlation-matrix-ggally-approach)
-   [Building a 2x2 Table](#building-a-2x2-table)
    -   [Standard Epidemiological Format](#standard-epidemiological-format)
    -   [Evaluating the 2x2 Table with the Epi package](#evaluating-the-2x2-table-with-the-epi-package)
-   [Building a Larger 2-way (also known as a 2-Factor) Table](#building-a-larger-2-way-also-known-as-a-2-factor-table)
    -   [Adding Marginal Counts](#adding-marginal-counts)
-   [Building a 3-way (Three-Factor) Table](#building-a-3-way-three-factor-table)
    -   [A Standard Table](#a-standard-table)
    -   [A Flattened Table](#a-flattened-table)
    -   [Getting the Counts in a Tibble](#getting-the-counts-in-a-tibble)
-   [Comparing Numerical Values for Different Categories](#comparing-numerical-values-for-different-categories)
    -   [A Bar Chart of Insurance Mix](#a-bar-chart-of-insurance-mix)
    -   [A Cleveland Dot Plot for Mean A1c by Insurance Type](#a-cleveland-dot-plot-for-mean-a1c-by-insurance-type)
    -   [Comparing the Sexes on Median A1c within Insurance Categories](#comparing-the-sexes-on-median-a1c-within-insurance-categories)
-   [Dealing with Missing Data - An Introduction](#dealing-with-missing-data---an-introduction)
    -   [Testing for Missing Values](#testing-for-missing-values)
    -   [The importance of `na.rm` and other commands for omitting missing values](#the-importance-of-na.rm-and-other-commands-for-omitting-missing-values)
    -   [Using Simple Imputation (generally a bad plan)](#using-simple-imputation-generally-a-bad-plan)
    -   [Using Multiple Imputation (generally a much better plan)](#using-multiple-imputation-generally-a-much-better-plan)
-   [Additional Issues](#additional-issues)
    -   [R ≠ R Studio ≠ R Markdown](#r-neq-r-studio-neq-r-markdown)
    -   [Producing Word files instead of HTML](#producing-word-files-instead-of-html)
    -   [Generating a PDF using R Markdown](#generating-a-pdf-using-r-markdown)

What is this?
=============

This is a way-too-long document demonstrating some things about working with data using R, R Studio and R Markdown. The first few sections are a good place to start. The rest provides lots and lots of code examples that may eventually help when doing assignments, etc., but are probably too much to read at one sitting.

Getting Started
===============

1.  Follow the [instructions to install R, R Studio and the R packages that we'll use in 431](https://github.com/THOMASELOVE/431/blob/master/software-installation-431.md). Once you have these things installed, you're ready for the steps below.
2.  Select or create a subdirectory on your computer for your project. We'll call that your **project folder**.
    -   Don't use the same subdirectory/folder for multiple projects.
    -   A good directory path might be something like `pqhs431/2017-08-29_my-first-R-project`
    -   You'll have a lot of projects over the course of the semester.
    -   You won't believe how important it is for you to understand where your files are and a well-designed naming scheme is an enormous time-saver. "A place for everything, and everything in its place" and all that...
    -   You want your names to be both "machine readable" and "human readable". Spaces in file names (including directory names) are evil. [See Jenny Bryan's advice on naming things](https://speakerdeck.com/jennybc/how-to-name-files).
3.  Use the **template** file we provide.
    -   As part of the general data and code provided at <https://github.com/THOMASELOVE/431data>, we provide a file called `431-r-template.Rmd` which will get you off to the right start for building a R Markdown file.
    -   We suggest you download the data and code (by clicking on the Clone or Download button then select Download ZIP) and then unzip the files on your computer, and copy the `431-r-template.Rmd` file to your **project folder** directory.
4.  Download the data you plan to use either into your chosen **project folder**, or to a subdirectory of that folder called **data**.
    -   Be sure you place this somewhere where you can find again later.
    -   Your data subdirectory might be `pqhs431/2017-08-29_my-first-R-project/data`, for example.
    -   Most of the data we will provide in 431 is in `.csv` format (comma-separated values) but R reads many other formats.
5.  Start R Studio and begin by opening up a **project**.
    -   Use **File ... New Project** to create a new project in your **project folder**.
        -   Create the R project in the main **project folder**, regardless of whether you've placed the data in that same folder, or in a data subdirectory of that folder.
        -   One and only one R Project per project folder is the way to happiness.
    -   When not doing this for the first time, use **File ... Open Project** to open an R Studio Project you've already created.

Editing the R Markdown file
===========================

A R Markdown file is just a plain text document, with interspersed R code that lets you produce reports that combine narration with results, and that can be easily exported as an HTML, Word or PDF file. It's a great tool. Dr. Love builds virtually everything you'll see in this class with R Markdown. R Markdown files use the `.Rmd` extension.

Open the template file `431-r-template.Rmd` by clicking on it in the **Files** tab on the lower right of your R Studio setup, or selecting **File ... Open** from the main menu. + The start of the template file is a top-line set of instructions to R Markdown about how to process the rest of the document. It is referred to as the YAML material, and looks like this:

    ---
    title: "R Markdown Template"
    author: "Your Name"
    date: "2017-08-27"
    output:
      html_document: 
        toc: yes
        code_folding: show
    ---

Now, edit the file to include a meaningful Title for this work, and place your actual name in the author section. Then use **File ... Save as** to save the Markdown file under a new project-specific name, rather than the generic `431-r-template.Rmd`. + Your result should look something like this:

In most cases, changing only the **title**, **author** and **date**, but otherwise leaving this as is, will work well for our purposes.

Loading in a Data Set
=====================

If you are reading in a comma separated version (`.csv`) data set for this course, first, be sure it is in the directory where R is looking for it. You can go to **Session ... Set Working Directory ... Choose Working Directory** if you need to change the directory R is looking at to something else. The directory you are using is usually specified at the top of the Files window on the lower right of R Studio.

To load the `.csv` data set called `dm120s.csv` into an R tibble named `dm120`, edit your template to look like this...

![Load the dm120s.csv data into the dm120 tibble](images/loaddm120s.png)

Now click on Knit at the top of the screen under the name of your file, and an HTML version should appear which includes the result that follows...

``` r
dm120 <- read_csv("data/dm120s.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   id = col_character(),
    ##   a1c = col_double(),
    ##   ldl = col_integer(),
    ##   sbp = col_integer(),
    ##   bmi = col_double(),
    ##   age = col_integer(),
    ##   sex = col_character(),
    ##   race.eth = col_character(),
    ##   insurance = col_character(),
    ##   smoking = col_character(),
    ##   eye.exam = col_character(),
    ##   pnvax = col_character()
    ## )

``` r
dm120
```

    ## # A tibble: 120 x 12
    ##        id   a1c   ldl   sbp   bmi   age    sex race.eth  insurance
    ##     <chr> <dbl> <int> <int> <dbl> <int>  <chr>    <chr>      <chr>
    ##  1 dm0001   8.3   108   112 23.68    23   male    White Commercial
    ##  2 dm0002   7.2   119   178 26.56    82 female    White   Medicare
    ##  3 dm0003   6.3    91   162 33.06    69 female    Black   Medicare
    ##  4 dm0004   9.5    85   124 41.30    46 female    White  Uninsured
    ##  5 dm0005   5.7   113   152 37.04    60 female    White Commercial
    ##  6 dm0006  10.6   162   126 43.13    52   male    White   Medicaid
    ##  7 dm0007   7.4   118   119 27.60    50   male Hispanic Commercial
    ##  8 dm0008   7.6    51   120 21.32    57   male    Black   Medicaid
    ##  9 dm0009  11.1   164   132 29.04    48   male Hispanic  Uninsured
    ## 10 dm0010   7.3   110   133 51.06    46 female    Black  Uninsured
    ## # ... with 110 more rows, and 3 more variables: smoking <chr>,
    ## #   eye.exam <chr>, pnvax <chr>

I'll use the `dm120` data in what follows...

Chunks of R Code
================

Your first chunk of R code should always look like this:

![Setup R and Load Packages](images/setup.png)

Of course, in many cases, you'll want to load more packages (libraries) than just `tidyverse` but in 431, at least, the `tidyverse` suite of packages is always necessary, and should be listed after any other packages you decide to load.

Chunk Options
-------------

To start a chunk of code in R, you have two options.

Either click on the Insert Chunk button (and select R) at the top of the R Markdown window within R Studio.

![The button looks like this](images/insertchunk1.png)

Or type in the following:

![Appearance of a standard chunk](images/insertchunk2.png)

and change the `chunkname` to something with meaning for you, consisting only of letters and numbers (no abbreviations and no commas.)

In either case, your R code then goes in the blank line in between the start and stop of the chunk. You can add more lines if you have longer code to write.

Chunks of Code, Interspersed with Text
--------------------------------------

In writing your R Markdown file, you will be interspersing code chunks with regular text, as shown here.

![](images/codeandtext.png)

The result will be

![](images/codeandtext2.png)

### Key Elements

-   Each chunk of code is separated out from the text by blank lines.
-   Each code chunk begins with the same three quote marks, a curved bracket and the letter r, followed by a name for the code chunk.
-   Each code chunk ends with three quote marks and a blank line, before text is written.
-   Each chunk of code is named. Do not repeat a name, or R Studio will throw an error.
-   Code chunks appear in gray, while text is shown without color in the background.
-   In text, each new section or subsection is set off using the hash symbol

<!-- -->

       # creates a main heading
       ## creates a level two heading
       ## creates a level three heading

-   In code chunks, the hash symbol indicates a comment, not to be executed by R.
-   Comments show up in a different color than other kinds of text while coding in R Studio.

Basic Numerical Summaries
=========================

``` r
summary(dm120)
```

    ##       id                 a1c              ldl             sbp       
    ##  Length:120         Min.   : 5.200   Min.   : 32.0   Min.   : 84.0  
    ##  Class :character   1st Qu.: 6.275   1st Qu.: 91.0   1st Qu.:120.0  
    ##  Mode  :character   Median : 7.100   Median :113.0   Median :130.0  
    ##                     Mean   : 7.748   Mean   :118.5   Mean   :136.0  
    ##                     3rd Qu.: 8.425   3rd Qu.:146.0   3rd Qu.:148.5  
    ##                     Max.   :15.400   Max.   :218.0   Max.   :213.0  
    ##                                      NA's   :11                     
    ##       bmi             age            sex              race.eth        
    ##  Min.   :16.62   Min.   :23.00   Length:120         Length:120        
    ##  1st Qu.:28.43   1st Qu.:48.00   Class :character   Class :character  
    ##  Median :33.50   Median :57.00   Mode  :character   Mode  :character  
    ##  Mean   :34.10   Mean   :57.26                                        
    ##  3rd Qu.:38.70   3rd Qu.:67.00                                        
    ##  Max.   :65.77   Max.   :84.00                                        
    ##                                                                       
    ##   insurance           smoking            eye.exam        
    ##  Length:120         Length:120         Length:120        
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character  
    ##                                                          
    ##                                                          
    ##                                                          
    ##                                                          
    ##     pnvax          
    ##  Length:120        
    ##  Class :character  
    ##  Mode  :character  
    ##                    
    ##                    
    ##                    
    ## 

``` r
dm120 %>% summarize(mean(a1c), sd(a1c), median(a1c))
```

    ## # A tibble: 1 x 3
    ##   `mean(a1c)` `sd(a1c)` `median(a1c)`
    ##         <dbl>     <dbl>         <dbl>
    ## 1    7.748333  2.154455           7.1

``` r
dm120 %>% summarize(quantile(a1c, 0.25), quantile(a1c, 0.75))
```

    ## # A tibble: 1 x 2
    ##   `quantile(a1c, 0.25)` `quantile(a1c, 0.75)`
    ##                   <dbl>                 <dbl>
    ## 1                 6.275                 8.425

``` r
IQR(dm120$a1c)
```

    ## [1] 2.15

``` r
dm120 %>%
  group_by(sex) %>%
  summarize(mean = mean(a1c), sd = sd(a1c))
```

    ## # A tibble: 2 x 3
    ##      sex     mean       sd
    ##    <chr>    <dbl>    <dbl>
    ## 1 female 7.836508 2.426421
    ## 2   male 7.650877 1.823960

On Rounding
-----------

``` r
mean(dm120$a1c) ## use the default number of decimal places
```

    ## [1] 7.748333

``` r
round(mean(dm120$a1c), 2) ## round to 2 decimal places
```

    ## [1] 7.75

``` r
signif(mean(dm120$a1c), 2) ## round to 2 significant figures
```

    ## [1] 7.7

Using Other Packages
--------------------

``` r
mosaic::favstats(dm120$a1c)
```

    ##  min    Q1 median    Q3  max     mean       sd   n missing
    ##  5.2 6.275    7.1 8.425 15.4 7.748333 2.154455 120       0

``` r
dm120 %>% 
    select(a1c, sbp, bmi, age) %>% 
    psych::describe()
```

    ##     vars   n   mean    sd median trimmed   mad   min    max  range  skew
    ## a1c    1 120   7.75  2.15    7.1    7.43  1.63  5.20  15.40  10.20  1.35
    ## sbp    2 120 135.97 23.15  130.0  134.51 17.79 84.00 213.00 129.00  0.65
    ## bmi    3 120  34.10  7.71   33.5   33.77  7.69 16.62  65.77  49.15  0.65
    ## age    4 120  57.26 14.14   57.0   57.61 14.08 23.00  84.00  61.00 -0.21
    ##     kurtosis   se
    ## a1c     1.53 0.20
    ## sbp     0.46 2.11
    ## bmi     1.47 0.70
    ## age    -0.42 1.29

``` r
dm120 %>%
    select(a1c, sex, insurance) %>%
    Hmisc::describe()
```

    ## . 
    ## 
    ##  3  Variables      120  Observations
    ## ---------------------------------------------------------------------------
    ## a1c 
    ##        n  missing distinct     Info     Mean      Gmd      .05      .10 
    ##      120        0       55    0.999    7.748    2.269    5.400    5.600 
    ##      .25      .50      .75      .90      .95 
    ##    6.275    7.100    8.425   11.120   11.930 
    ## 
    ## lowest :  5.2  5.4  5.5  5.6  5.7, highest: 12.8 13.7 14.0 14.4 15.4
    ## ---------------------------------------------------------------------------
    ## sex 
    ##        n  missing distinct 
    ##      120        0        2 
    ##                         
    ## Value      female   male
    ## Frequency      63     57
    ## Proportion  0.525  0.475
    ## ---------------------------------------------------------------------------
    ## insurance 
    ##        n  missing distinct 
    ##      120        0        4 
    ##                                                       
    ## Value      Commercial   Medicaid   Medicare  Uninsured
    ## Frequency          33         19         42         26
    ## Proportion      0.275      0.158      0.350      0.217
    ## ---------------------------------------------------------------------------

Functions from Dr. Love
=======================

skew1
-----

The `skew1` function provides the skew1 measure (mean - median divided by sd)

``` r
skew1 <- function(x, na.rm=FALSE) {
  a <- (mean(x) - median(x))/sd(x)
  return(a)
}
```

Emp\_Rule: Does the 68-95-99.7 "Empirical Rule" Work Well for these Data?
-------------------------------------------------------------------------

Let's look at the `a1c` data across all of the `dm120` subjects.

``` r
## requires that the pander library is installed
Emp_Rule <- function(x, na.rm=FALSE) {
  tmp.overall_n <- length(x)
  tmp.mean <- mean(x)
  tmp.sd <- sd(x)
  tmp.in1sd <- length(x[x > tmp.mean - tmp.sd & 
                                 x < tmp.mean + tmp.sd])
  tmp.in2sd <- length(x[x > tmp.mean - 2*tmp.sd & 
                                 x < tmp.mean + 2*tmp.sd])
  tmp.in3sd <- length(x[x > tmp.mean - 3*tmp.sd & 
                                 x < tmp.mean + 3*tmp.sd])
  tmp.prop1sd <- tmp.in1sd / tmp.overall_n
  tmp.prop2sd <- tmp.in2sd / tmp.overall_n
  tmp.prop3sd <- tmp.in3sd / tmp.overall_n
  res.count <- c(tmp.in1sd, tmp.in2sd, tmp.in3sd, tmp.overall_n)
  res.prop <- c(tmp.prop1sd, tmp.prop2sd, tmp.prop3sd, 1)
  res.exp <- c(0.68, 0.95, 0.997, 1)
  res <- data.frame(count = res.count, proportion = res.prop)
  row.names(res) <- c("Mean +/- 1 SD", "Mean +/- 2 SD", "Mean +/- 3 SD", "Entire Data Set")
  return(pander::pander(res))
  rm(tmp.overall_n, tmp.mean, tmp.sd, tmp.in1sd, tmp.in2sd, tmp.in3sd,
     tmp.prop1sd, tmp.prop2sd, tmp.prop3sd, res.count, res.prop, res)
}
```

Here are our results.

``` r
Emp_Rule(dm120$a1c)
```

<table style="width:58%;">
<colgroup>
<col width="30%" />
<col width="11%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="center"> </th>
<th align="center">count</th>
<th align="center">proportion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center"><strong>Mean +/- 1 SD</strong></td>
<td align="center">91</td>
<td align="center">0.7583</td>
</tr>
<tr class="even">
<td align="center"><strong>Mean +/- 2 SD</strong></td>
<td align="center">114</td>
<td align="center">0.95</td>
</tr>
<tr class="odd">
<td align="center"><strong>Mean +/- 3 SD</strong></td>
<td align="center">118</td>
<td align="center">0.9833</td>
</tr>
<tr class="even">
<td align="center"><strong>Entire Data Set</strong></td>
<td align="center">120</td>
<td align="center">1</td>
</tr>
</tbody>
</table>

Assessing Correlations
======================

Pearson Correlations
--------------------

``` r
cor(dm120$a1c, dm120$sbp)
```

    ## [1] 0.04014063

``` r
dm120 %>%
  select(a1c, sbp, bmi) %>%
  cor(use = "complete.obs")
```

    ##             a1c        sbp         bmi
    ## a1c  1.00000000 0.04014063 -0.06034192
    ## sbp  0.04014063 1.00000000  0.16794021
    ## bmi -0.06034192 0.16794021  1.00000000

Spearman Correlations
---------------------

``` r
cor(dm120$a1c, dm120$sbp, method = "spearman")
```

    ## [1] 0.001948152

``` r
dm120 %>%
  select(a1c, sbp, bmi) %>%
  cor(method = "spearman", use = "complete.obs") %>%
  round(digits = 3)
```

    ##        a1c   sbp    bmi
    ## a1c  1.000 0.002 -0.013
    ## sbp  0.002 1.000  0.162
    ## bmi -0.013 0.162  1.000

Plotting a Single Batch of Data
===============================

For all plots, I cannot recommend the R Studio Data Visualization with ggplot2 Cheat Sheet enough. There's a link on our website, but this can also be reached through the **Help ... Cheat Sheets** menu in R Studio.

Histogram
---------

``` r
ggplot(dm120, aes(x = a1c)) +
    geom_histogram(bins = 20, fill = "dodgerblue", col = "navy")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/histogram%20of%20Hemoglobin%20A1c-1.png)

to which we can add titles, subtitles, captions, and axis labels

``` r
ggplot(dm120, aes(x = a1c)) +
    geom_histogram(bins = 20, fill = "dodgerblue", col = "navy") +
    labs(x = "Hemoglobin A1c level (%)",
         y = "Number of Observations",
         title = "Histogram of A1c data",
         subtitle = "from the dm120 data set",
         caption = "The data describe 120 adults with diabetes.")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/histogram%20of%20Hemoglobin%20A1c%20with%20labels%20etc-1.png)

Frequency Polygon
-----------------

``` r
ggplot(dm120, aes(x = a1c)) +
  geom_freqpoly(bins = 12, col = "navy")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/frequency%20polygon%20for%20Hemoglobin%20A1c-1.png)

Density Plot
------------

``` r
ggplot(dm120, aes(x = a1c)) +
  geom_density(col = "salmon", size = 2)
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/density%20plot%20of%20Hemoglobin%20A1c-1.png)

Comparing a Histogram to a Normal Model
---------------------------------------

``` r
ggplot(dm120, aes(x = a1c)) +
  geom_histogram(aes(y = ..density..), bins=12, fill = "wheat", color = "navy") +
  stat_function(fun = dnorm,
                args = list(mean = mean(dm120$a1c), 
                            sd = sd(dm120$a1c)),
                lwd = 1.5, col = "red") +
  geom_text(aes(label = paste("Mean", round(mean(dm120$a1c),1),
                              ", SD", round(sd(dm120$a1c),1))),
            x = 7, y = 0.4, color="red", fontface = "italic") +
  labs(title = "A1c with Normal Distribution Superimposed",
       x = "Hemoglobin A1c (%)", 
       y = "Probability Density Function")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/histogram%20with%20normal%20density%20superimposed-1.png)

Boxplot for a Single Batch of Data
----------------------------------

``` r
ggplot(dm120, aes(x = 1, y = a1c)) +
  geom_boxplot(fill = "cyan") +
  coord_flip() +
  theme(axis.text.y = element_blank(), axis.ticks.y = element_blank()) +
  labs(title = "Boxplot of dm120 Hemoglobin A1c",
       y = "Hemoglobin A1c (%)", x = "")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/ggplot%20boxplot%20for%20a1c-1.png)

Stem and Leaf Display
---------------------

``` r
stem(dm120$a1c)
```

    ## 
    ##   The decimal point is at the |
    ## 
    ##    5 | 22224445555667778888
    ##    6 | 0001112222333344555555667777788889999
    ##    7 | 0111233334456667777899
    ##    8 | 01333333444567899
    ##    9 | 035678
    ##   10 | 12269
    ##   11 | 1333599
    ##   12 | 58
    ##   13 | 7
    ##   14 | 04
    ##   15 | 4

Dot Plot
--------

``` r
ggplot(dm120, aes(x = a1c)) +
  geom_dotplot(binwidth = 0.25) + 
  scale_y_continuous(NULL, breaks = NULL)
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/dot%20plot-1.png)

Building Plots to Assess Normality and Transformations
======================================================

Normal Q-Q Plot (using the ggplot2 library)
-------------------------------------------

``` r
ggplot(dm120, aes(sample = a1c)) +
  geom_qq(size = 2)
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/normal%20qq%20plot%20with%20ggplot2-1.png)

Normal Q-Q Plot (without the ggplot2 library)
---------------------------------------------

We have a base graphics solution for a Normal Q-Q plot that is simpler than the `ggplot` approach.

``` r
qqnorm(dm120$a1c, main = "Normal Q-Q Plot for dm120 Hemoglobin A1c")
qqline(dm120$a1c, col = "red")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/normal%20qq%20plot%20without%20ggplot2-1.png)

Plotting Multiple Plots in the Same Figure
==========================================

Suppose we wanted to place multiple plots in one Figure, all drawn using `ggplot2`. We can do this using the `grid.arrange` function from the `gridExtra` package.

``` r
p1 <- ggplot(dm120, aes(x = a1c)) +
  geom_histogram(bins = 10, fill = "royalblue", col = "black") +
  labs(title = "Histogram", x = "Hemoglobin A1c (%)")
  
p2 <- ggplot(dm120, aes(x = 1, y = a1c)) +
  geom_boxplot(notch = TRUE, fill = "royalblue") +
  theme(axis.text.x = element_blank(), axis.ticks.x = element_blank()) +
  labs(title = "Boxplot",
       y = "Hemoglobin A1c (%)", x = "")

p3 <- ggplot(dm120, aes(sample = a1c)) +
  geom_qq(col = "royalblue") + 
  labs(title = "Normal Q-Q Plot", y = "Sorted Hemoglobin A1c (%)")

gridExtra::grid.arrange(p1, p2, p3, nrow = 1,
             top = "dm120 Hemoglobin A1c Values" )
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/plot%20three%20ggplots%20together-1.png)

Of course, we could and should build more informative titles for the individual plots.

Plotting Nine Plots in the Same Figure (Ladder of Power Transformations)
------------------------------------------------------------------------

Let's investigate the impact of the ladder of power transformations on these data, assessing whether a Normal model would be appropriate, either for the raw data or for some transformation.

``` r
p1 <- ggplot(dm120, aes(x = a1c^3)) + geom_freqpoly(bins=12, col = "blue")
p2 <- ggplot(dm120, aes(x = a1c^2)) + geom_freqpoly(bins=12, col = "red")
p3 <- ggplot(dm120, aes(x = a1c)) + geom_freqpoly(bins=12, col = "black", size = 2)
p4 <- ggplot(dm120, aes(x = sqrt(a1c))) + geom_freqpoly(bins=12, col = "blue")
p5 <- ggplot(dm120, aes(x = log(a1c))) + geom_freqpoly(bins=12, col = "red")
p6 <- ggplot(dm120, aes(x = 1/sqrt(a1c))) + geom_freqpoly(bins=12, col = "purple")
p7 <- ggplot(dm120, aes(x = 1/a1c)) + geom_freqpoly(bins=12, col = "blue")
p8 <- ggplot(dm120, aes(x = 1/(a1c^2))) + geom_freqpoly(bins=12, col = "red")
p9 <- ggplot(dm120, aes(x = 1/(a1c^3))) + geom_freqpoly(bins=12, col = "purple")

gridExtra::grid.arrange(p1, p2, p3, p4, p5, p6, p7, p8, p9, nrow=3, 
            top="Ladder of Power Transformations for dm120 A1c values")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/example%201%20entire%20ladder%20of%20frequency%20polygons-1.png)

When we're done with this plot, we should clean up after ourselves, or we'll continue to have these p1...p9 objects cluttering up our environment. We created nine new plots. Let's remove them from the environment with the `rm` function.

``` r
rm(p1, p2, p3, p4, p5, p6, p7, p8, p9)
```

Plotting a Quantitative Outcome and a Categorical Predictor
===========================================================

Comparison Boxplot with Notches
-------------------------------

Let's compare the three race/ethnicity groups in the `dm120` data on their A1c values.

``` r
ggplot(dm120, aes(x = race.eth, y = a1c, fill = race.eth)) +
  geom_boxplot(notch = TRUE) + 
  guides(fill = FALSE) +
  labs(x = "Race/Ethnicity Category", y = "Hemoglobin A1c (%)")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/comparison%20boxplot-1.png)

Using a Violin Plot to Compare Distributions
--------------------------------------------

``` r
ggplot(dm120, aes(x = race.eth, y = a1c, fill = race.eth)) +
  geom_violin(trim=FALSE) +
  geom_boxplot(width=.2, outlier.colour=NA, color = "black", notch=TRUE) +
  stat_summary(fun.y=median, geom="point", fill="white", shape=21, size=3) +
  guides(fill = FALSE) +
  labs(x = "Race/Ethnicity Category", y = "Hemoglobin A1c (%)")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/violin%20plot-1.png)

Comparing Distributions with Faceted Histograms
-----------------------------------------------

``` r
ggplot(dm120, aes(x=a1c, fill = race.eth)) +
  geom_histogram(bins = 7, col = "white") + 
  guides(fill = FALSE) +
  facet_wrap(~ race.eth)
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/comparing%20with%20faceted%20histograms-1.png)

Faceted Density Plots
---------------------

``` r
ggplot(dm120, aes(x=a1c, fill = insurance)) +
  geom_density() +
  guides(fill = FALSE) +
  facet_wrap(~ insurance) +
  labs(x = "Hemoglobin A1c (%)", y = "Probability Density Function")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/comparing%20with%20faceted%20density%20plots-1.png)

Joy Plot
--------

``` r
ggplot(dm120, aes(x = a1c, y = insurance, fill = insurance)) +
  ggjoy::geom_joy(scale = 1) +
  guides(fill = FALSE) +
  labs(x = "Hemoglobin A1c (%)", y = "",
       title = "Hemoglobin A1c by Insurance type, dm120 data",
       subtitle = "A Joy Plot") 
```

    ## Picking joint bandwidth of 0.738

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/comparing%20with%20joy%20plot-1.png)

Plotting a Quantitative Outcome and a Quantitative Predictor
============================================================

Scatterplot with loess smooth
-----------------------------

``` r
ggplot(dm120, aes(x = sbp, y = a1c)) +
  geom_point() +
  geom_smooth(col = "blue") +
  labs(title = "Predicting A1c using Systolic BP, with loess smooth",
       x = "Systolic Blood Pressure (mm Hg)", y = "Hemoglobin A1c (%)")
```

    ## `geom_smooth()` using method = 'loess'

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/scatterplot%20with%20loess-1.png)

Scatterplot with linear fit
---------------------------

``` r
ggplot(dm120, aes(x = sbp, y = a1c)) +
  geom_point() +
  geom_smooth(method = "lm", col = "red") +
  labs(title = "Linear Fit predicting A1c using Systolic BP",
       x = "Systolic Blood Pressure (mm Hg)", y = "Hemoglobin A1c (%)")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/scatterplot%20with%20linear%20fit-1.png)

Fitting a Linear Model to Describe the Association
==================================================

``` r
model1 <- with(dm120, lm(a1c ~ sbp))
model1 
```

    ## 
    ## Call:
    ## lm(formula = a1c ~ sbp)
    ## 
    ## Coefficients:
    ## (Intercept)          sbp  
    ##    7.240512     0.003735

``` r
summary(model1) 
```

    ## 
    ## Call:
    ## lm(formula = a1c ~ sbp)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -2.5858 -1.5092 -0.7138  0.6990  7.6814 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 7.240512   1.180300   6.134 1.17e-08 ***
    ## sbp         0.003735   0.008559   0.436    0.663    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 2.162 on 118 degrees of freedom
    ## Multiple R-squared:  0.001611,   Adjusted R-squared:  -0.00685 
    ## F-statistic: 0.1904 on 1 and 118 DF,  p-value: 0.6634

Making Predictions
------------------

Suppose we want to predict the Hemoglobin A1c for a new subject with systolic blood pressure of 140 using our model?

-   If we are predicting the Hemoglobin A1c of a single new subject with sbp of 140, we'd use a prediction interval

``` r
predict(model1, newdata = data.frame(sbp = 140), 
        level = 0.95, interval = "prediction")
```

    ##        fit      lwr      upr
    ## 1 7.763397 3.464059 12.06274

-   If we are predicting the average A1c across all subjects in a large population who have SBP = 140, we would then use a confidence interval

``` r
predict(model1, newdata = data.frame(sbp = 140), 
        level = 0.95, interval = "confidence")
```

    ##        fit      lwr      upr
    ## 1 7.763397 7.366664 8.160131

``` r
rm(model1)
```

Adding in a Categorical Predictor
=================================

Scatterplots faceted by a Categorical Predictor
-----------------------------------------------

``` r
ggplot(dm120, aes(x = sbp, y = a1c, col = insurance)) +
  geom_point() +
  geom_smooth(se = FALSE) +
  guides(color = FALSE) +
  facet_wrap(~ insurance) +
  labs(title = "Predicting A1c using SBP by insurance, with loess smooth")
```

    ## `geom_smooth()` using method = 'loess'

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/faceted%20scatterplots%20with%20loess-1.png)

Scatterplots showing Multiple Categories at once
------------------------------------------------

``` r
ggplot(dm120, aes(x = sbp, y = a1c, col = insurance)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE) +
  labs(title = "Insurance-Specific Linear Fits of A1c by SBP",
       x = "Systolic Blood Pressure (mm Hg)", y = "Hemoglobin A1c (%)")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/scatterplots%20showing%20each%20insurance%20with%20loess-1.png)

Fitting a Linear Model to account for one Quantitative Predictor, one Categorical Predictor and their Interaction
=================================================================================================================

``` r
model2 <- with(dm120, lm(a1c ~ sbp * insurance))
pander::pander(model2) # much prettier
```

<table>
<caption>Fitting linear model: a1c ~ sbp * insurance</caption>
<colgroup>
<col width="39%" />
<col width="16%" />
<col width="17%" />
<col width="13%" />
<col width="13%" />
</colgroup>
<thead>
<tr class="header">
<th align="center"> </th>
<th align="center">Estimate</th>
<th align="center">Std. Error</th>
<th align="center">t value</th>
<th align="center">Pr(&gt;|t|)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center"><strong>(Intercept)</strong></td>
<td align="center">7.536</td>
<td align="center">2.312</td>
<td align="center">3.26</td>
<td align="center">0.001477</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp</strong></td>
<td align="center">-0.002718</td>
<td align="center">0.01723</td>
<td align="center">-0.1578</td>
<td align="center">0.8749</td>
</tr>
<tr class="odd">
<td align="center"><strong>insuranceMedicaid</strong></td>
<td align="center">5.161</td>
<td align="center">4.358</td>
<td align="center">1.184</td>
<td align="center">0.2388</td>
</tr>
<tr class="even">
<td align="center"><strong>insuranceMedicare</strong></td>
<td align="center">-0.832</td>
<td align="center">2.937</td>
<td align="center">-0.2833</td>
<td align="center">0.7775</td>
</tr>
<tr class="odd">
<td align="center"><strong>insuranceUninsured</strong></td>
<td align="center">-0.5066</td>
<td align="center">3.349</td>
<td align="center">-0.1513</td>
<td align="center">0.88</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp:insuranceMedicaid</strong></td>
<td align="center">-0.03891</td>
<td align="center">0.03227</td>
<td align="center">-1.205</td>
<td align="center">0.2306</td>
</tr>
<tr class="odd">
<td align="center"><strong>sbp:insuranceMedicare</strong></td>
<td align="center">0.01179</td>
<td align="center">0.02144</td>
<td align="center">0.55</td>
<td align="center">0.5834</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp:insuranceUninsured</strong></td>
<td align="center">0.01416</td>
<td align="center">0.02462</td>
<td align="center">0.5748</td>
<td align="center">0.5665</td>
</tr>
</tbody>
</table>

``` r
pander::pander(summary(model2))
```

<table>
<colgroup>
<col width="39%" />
<col width="16%" />
<col width="17%" />
<col width="13%" />
<col width="13%" />
</colgroup>
<thead>
<tr class="header">
<th align="center"> </th>
<th align="center">Estimate</th>
<th align="center">Std. Error</th>
<th align="center">t value</th>
<th align="center">Pr(&gt;|t|)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center"><strong>(Intercept)</strong></td>
<td align="center">7.536</td>
<td align="center">2.312</td>
<td align="center">3.26</td>
<td align="center">0.001477</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp</strong></td>
<td align="center">-0.002718</td>
<td align="center">0.01723</td>
<td align="center">-0.1578</td>
<td align="center">0.8749</td>
</tr>
<tr class="odd">
<td align="center"><strong>insuranceMedicaid</strong></td>
<td align="center">5.161</td>
<td align="center">4.358</td>
<td align="center">1.184</td>
<td align="center">0.2388</td>
</tr>
<tr class="even">
<td align="center"><strong>insuranceMedicare</strong></td>
<td align="center">-0.832</td>
<td align="center">2.937</td>
<td align="center">-0.2833</td>
<td align="center">0.7775</td>
</tr>
<tr class="odd">
<td align="center"><strong>insuranceUninsured</strong></td>
<td align="center">-0.5066</td>
<td align="center">3.349</td>
<td align="center">-0.1513</td>
<td align="center">0.88</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp:insuranceMedicaid</strong></td>
<td align="center">-0.03891</td>
<td align="center">0.03227</td>
<td align="center">-1.205</td>
<td align="center">0.2306</td>
</tr>
<tr class="odd">
<td align="center"><strong>sbp:insuranceMedicare</strong></td>
<td align="center">0.01179</td>
<td align="center">0.02144</td>
<td align="center">0.55</td>
<td align="center">0.5834</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp:insuranceUninsured</strong></td>
<td align="center">0.01416</td>
<td align="center">0.02462</td>
<td align="center">0.5748</td>
<td align="center">0.5665</td>
</tr>
</tbody>
</table>

<table style="width:88%;">
<caption>Fitting linear model: a1c ~ sbp * insurance</caption>
<colgroup>
<col width="20%" />
<col width="30%" />
<col width="13%" />
<col width="22%" />
</colgroup>
<thead>
<tr class="header">
<th align="center">Observations</th>
<th align="center">Residual Std. Error</th>
<th align="center"><span class="math inline"><em>R</em><sup>2</sup></span></th>
<th align="center">Adjusted <span class="math inline"><em>R</em><sup>2</sup></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center">120</td>
<td align="center">2.111</td>
<td align="center">0.09644</td>
<td align="center">0.03997</td>
</tr>
</tbody>
</table>

Making Predictions using Model 2
--------------------------------

Suppose we want to predict the Hemoglobin A1c for a new subject with SBP = 140, for each possible insurance type, using our new model 2?

-   If we are predicting the Hemoglobin A1c of a single new subject with SBP = 140, for each possible insurance type, we'd use a prediction interval

First, we create a data set of new values for which we want to predict.

``` r
dm120.newdata <- data.frame(sbp = c(140, 140, 140, 140), 
        insurance = c("Medicare", "Commercial", "Medicaid", "Uninsured"))
rownames(dm120.newdata) <- dm120.newdata$insurance
dm120.newdata
```

    ##            sbp  insurance
    ## Medicare   140   Medicare
    ## Commercial 140 Commercial
    ## Medicaid   140   Medicaid
    ## Uninsured  140  Uninsured

Then, we apply `model2` to these new data, and obtain prediction intervals.

``` r
predict(model2, newdata = dm120.newdata, level = 0.95, interval = "prediction")
```

    ##                 fit      lwr      upr
    ## Medicare   7.974237 3.742124 12.20635
    ## Commercial 7.155330 2.902080 11.40858
    ## Medicaid   6.869546 2.566879 11.17221
    ## Uninsured  8.630477 4.365503 12.89545

-   If we are predicting the average Hemoglobin A1c of all possible subjects with SBP = 140, for each possible insurance type, we would then use a confidence interval

``` r
predict(model2, newdata = dm120.newdata, level = 0.95, interval = "confidence")
```

    ##                 fit      lwr      upr
    ## Medicare   7.974237 7.328800 8.619675
    ## Commercial 7.155330 6.383363 7.927297
    ## Medicaid   6.869546 5.860214 7.878878
    ## Uninsured  8.630477 7.796324 9.464630

Can we neaten up the presentation by rounding the results to three significant figures, and then display the resulting table using the `pander` package?

``` r
temp <- predict(model2, newdata = dm120.newdata, 
                level = 0.95, interval = "confidence")

pander::pander(signif(temp,3))
```

<table style="width:53%;">
<colgroup>
<col width="23%" />
<col width="9%" />
<col width="9%" />
<col width="9%" />
</colgroup>
<thead>
<tr class="header">
<th align="center"> </th>
<th align="center">fit</th>
<th align="center">lwr</th>
<th align="center">upr</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center"><strong>Medicare</strong></td>
<td align="center">7.97</td>
<td align="center">7.33</td>
<td align="center">8.62</td>
</tr>
<tr class="even">
<td align="center"><strong>Commercial</strong></td>
<td align="center">7.16</td>
<td align="center">6.38</td>
<td align="center">7.93</td>
</tr>
<tr class="odd">
<td align="center"><strong>Medicaid</strong></td>
<td align="center">6.87</td>
<td align="center">5.86</td>
<td align="center">7.88</td>
</tr>
<tr class="even">
<td align="center"><strong>Uninsured</strong></td>
<td align="center">8.63</td>
<td align="center">7.8</td>
<td align="center">9.46</td>
</tr>
</tbody>
</table>

``` r
rm(temp, model2, dm120.newdata)
```

Plotting the Association of Multiple Variables
==============================================

A Scatterplot Matrix (GGally approach)
--------------------------------------

The `ggpairs` function from the `GGally` package provides a density plot on each diagonal, Pearson correlations on the upper right and scatterplots on the lower left of the matrix for the quantitative variables. What does this do for the binary factor `smoking`?

``` r
temp <- dm120 %>%
  select(a1c, sbp, bmi, smoking)

# next line requires GGally package be loaded
GGally::ggpairs(temp, title = "Scatterplot Matrix for dm120 subjects")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/GGally%20scatterplot%20matrix-1.png)

Plotting a Correlation Matrix (GGally approach)
-----------------------------------------------

Here, I will drop the categorical variable `smoking`, since we're just looking at correlations, but add in the other quantitative variables in the `dm120` data, specifically the subject's `age` and `ldl` cholesterol level.

``` r
temp <- dm120 %>%
  select(a1c, sbp, bmi, ldl, age)

GGally::ggcorr(temp, name = "Pearson r", label = TRUE)
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/GGally%20correlation%20matrix-1.png)

``` r
pander::pander(cor(temp, use = "complete.obs"), digits = 2)
```

<table style="width:75%;">
<colgroup>
<col width="13%" />
<col width="12%" />
<col width="11%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="center"> </th>
<th align="center">a1c</th>
<th align="center">sbp</th>
<th align="center">bmi</th>
<th align="center">ldl</th>
<th align="center">age</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center"><strong>a1c</strong></td>
<td align="center">1</td>
<td align="center">0.032</td>
<td align="center">-0.097</td>
<td align="center">0.3</td>
<td align="center">0.11</td>
</tr>
<tr class="even">
<td align="center"><strong>sbp</strong></td>
<td align="center">0.032</td>
<td align="center">1</td>
<td align="center">0.19</td>
<td align="center">0.15</td>
<td align="center">0.27</td>
</tr>
<tr class="odd">
<td align="center"><strong>bmi</strong></td>
<td align="center">-0.097</td>
<td align="center">0.19</td>
<td align="center">1</td>
<td align="center">-0.028</td>
<td align="center">-0.23</td>
</tr>
<tr class="even">
<td align="center"><strong>ldl</strong></td>
<td align="center">0.3</td>
<td align="center">0.15</td>
<td align="center">-0.028</td>
<td align="center">1</td>
<td align="center">0.17</td>
</tr>
<tr class="odd">
<td align="center"><strong>age</strong></td>
<td align="center">0.11</td>
<td align="center">0.27</td>
<td align="center">-0.23</td>
<td align="center">0.17</td>
<td align="center">1</td>
</tr>
</tbody>
</table>

``` r
rm(temp)
```

Building a 2x2 Table
====================

Here is a two-by-two table of smoking status by eye examination.

``` r
table(dm120$smoking, dm120$eye.exam)
```

    ##            
    ##             no yes
    ##   nonsmoker 58  23
    ##   smoker    32   7

This simple table, with two rows and two columns, is called a *two-by-two table*.

Standard Epidemiological Format
-------------------------------

**Standard Epidemiological Format** means that the predictor is in the rows, with either the more common category or the more interesting category at the top, and that the outcome is in the columns, with the more common or more interesting column on the left. Thus, the most interesting combination is top left. To try to predict the relationship between getting an Eye Exam and being a smoker, we'd like to have the people who smoke in the top row, and those who receive Eye exams on the left.

``` r
dm120$sm <- factor(dm120$smoking, levels = c("smoker", "nonsmoker"))
dm120$eye <- factor(dm120$eye.exam, levels = c("yes", "no"))
tab1 <- table(dm120$sm, dm120$eye)
pander::pander(tab1)
```

<table style="width:39%;">
<colgroup>
<col width="22%" />
<col width="8%" />
<col width="8%" />
</colgroup>
<thead>
<tr class="header">
<th align="center"> </th>
<th align="center">yes</th>
<th align="center">no</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center"><strong>smoker</strong></td>
<td align="center">7</td>
<td align="center">32</td>
</tr>
<tr class="even">
<td align="center"><strong>nonsmoker</strong></td>
<td align="center">23</td>
<td align="center">58</td>
</tr>
</tbody>
</table>

Evaluating the 2x2 Table with the Epi package
---------------------------------------------

``` r
Epi::twoby2(tab1)
```

    ## 2 by 2 table analysis: 
    ## ------------------------------------------------------ 
    ## Outcome   : yes 
    ## Comparing : smoker vs. nonsmoker 
    ## 
    ##           yes no    P(yes) 95% conf. interval
    ## smoker      7 32    0.1795    0.0881   0.3314
    ## nonsmoker  23 58    0.2840    0.1966   0.3913
    ## 
    ##                                     95% conf. interval
    ##              Relative Risk:  0.6321    0.2971   1.3447
    ##          Sample Odds Ratio:  0.5516    0.2134   1.4260
    ## Conditional MLE Odds Ratio:  0.5542    0.1805   1.5238
    ##     Probability difference: -0.1045   -0.2435   0.0663
    ## 
    ##              Exact P-value: 0.2644 
    ##         Asymptotic P-value: 0.2196 
    ## ------------------------------------------------------

Building a Larger 2-way (also known as a 2-Factor) Table
========================================================

Here is another two-way table - this one is a 3x4 table, since it has 3 rows (race/ethnicity groups) and 4 columns (insurance categories)

``` r
dm120 %>%
    select(race.eth, insurance) %>%
    table()
```

    ##           insurance
    ## race.eth   Commercial Medicaid Medicare Uninsured
    ##   Black             7       13       18        16
    ##   Hispanic          4        2        3         2
    ##   White            22        4       21         8

Adding Marginal Counts
----------------------

``` r
dm120 %>%
    select(race.eth, insurance) %>%
    table() %>%
    addmargins()
```

    ##           insurance
    ## race.eth   Commercial Medicaid Medicare Uninsured Sum
    ##   Black             7       13       18        16  54
    ##   Hispanic          4        2        3         2  11
    ##   White            22        4       21         8  55
    ##   Sum              33       19       42        26 120

Building a 3-way (Three-Factor) Table
=====================================

Next, we'll build a table to show three factors: `sex`, `insurance` and `smoking`, making this a three-way table.

A Standard Table
----------------

``` r
dm120 %>%
    select(smoking, insurance, sex) %>%
    table()
```

    ## , , sex = female
    ## 
    ##            insurance
    ## smoking     Commercial Medicaid Medicare Uninsured
    ##   nonsmoker         12        7       14        13
    ##   smoker             8        2        3         4
    ## 
    ## , , sex = male
    ## 
    ##            insurance
    ## smoking     Commercial Medicaid Medicare Uninsured
    ##   nonsmoker          7        6       16         6
    ##   smoker             6        4        9         3

A Flattened Table
-----------------

``` r
dm120 %>%
    select(smoking, insurance, sex) %>%
    ftable()
```

    ##                      sex female male
    ## smoking   insurance                 
    ## nonsmoker Commercial         12    7
    ##           Medicaid            7    6
    ##           Medicare           14   16
    ##           Uninsured          13    6
    ## smoker    Commercial          8    6
    ##           Medicaid            2    4
    ##           Medicare            3    9
    ##           Uninsured           4    3

Getting the Counts in a Tibble
------------------------------

``` r
dm120 %>%
    count(smoking, insurance, sex) 
```

    ## # A tibble: 16 x 4
    ##      smoking  insurance    sex     n
    ##        <chr>      <chr>  <chr> <int>
    ##  1 nonsmoker Commercial female    12
    ##  2 nonsmoker Commercial   male     7
    ##  3 nonsmoker   Medicaid female     7
    ##  4 nonsmoker   Medicaid   male     6
    ##  5 nonsmoker   Medicare female    14
    ##  6 nonsmoker   Medicare   male    16
    ##  7 nonsmoker  Uninsured female    13
    ##  8 nonsmoker  Uninsured   male     6
    ##  9    smoker Commercial female     8
    ## 10    smoker Commercial   male     6
    ## 11    smoker   Medicaid female     2
    ## 12    smoker   Medicaid   male     4
    ## 13    smoker   Medicare female     3
    ## 14    smoker   Medicare   male     9
    ## 15    smoker  Uninsured female     4
    ## 16    smoker  Uninsured   male     3

Comparing Numerical Values for Different Categories
===================================================

A Bar Chart of Insurance Mix
----------------------------

``` r
ggplot(dm120, aes(x = insurance, fill = insurance)) +
  geom_bar() + 
  guides(fill = FALSE)
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/ggplot%20of%20insurance%20types-1.png)

A Cleveland Dot Plot for Mean A1c by Insurance Type
---------------------------------------------------

Suppose we calculate the mean Hemoglobin A1c value for each of our four insurance types, and then want to plot this in a way that will be easy to review.

``` r
dm120 %>%
  group_by(insurance) %>%
  summarize(mean.A1c = mean(a1c))
```

    ## # A tibble: 4 x 2
    ##    insurance mean.A1c
    ##        <chr>    <dbl>
    ## 1 Commercial 7.175758
    ## 2   Medicaid 7.110526
    ## 3   Medicare 7.971429
    ## 4  Uninsured 8.580769

This is a Cleveland dot plot of these means, where I've rearranged the insurance levels to reflect the mean A1c in each insurance group.

``` r
dm120 %>%
    group_by(insurance) %>%
    summarize(mean.A1c = mean(a1c)) %>%
    ggplot(., aes(x = mean.A1c, y = reorder(insurance, mean.A1c))) +
    geom_point(size = 3) + 
    labs(x = "Mean Hemoglobin A1c in the dm120 data", 
         y = "Insurance Category")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/cleveland%20dot%20plot-1.png)

Comparing the Sexes on Median A1c within Insurance Categories
-------------------------------------------------------------

``` r
dm120 %>%
  group_by(insurance, sex) %>%
  summarize(median.A1c = median(a1c))
```

    ## # A tibble: 8 x 3
    ## # Groups:   insurance [?]
    ##    insurance    sex median.A1c
    ##        <chr>  <chr>      <dbl>
    ## 1 Commercial female       6.70
    ## 2 Commercial   male       6.70
    ## 3   Medicaid female       6.50
    ## 4   Medicaid   male       7.65
    ## 5   Medicare female       7.20
    ## 6   Medicare   male       7.40
    ## 7  Uninsured female       8.30
    ## 8  Uninsured   male       8.70

``` r
dm120 %>%
    group_by(insurance, sex) %>%
    summarize(median.A1c = median(a1c)) %>%
    ggplot(., aes(x = median.A1c, y = reorder(insurance, median.A1c), 
                   col = sex)) +
    geom_point(size = 3) + 
    labs(x = "Median Hemoglobin A1c in the dm120 data", 
         y = "Insurance Category",
         title = "A1c by Insurance and Sex")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/cleveland%20dot%20plot%202-1.png)

Dealing with Missing Data - An Introduction
===========================================

Data values that are missing are indicated in R, and to R, by the symbol `NA`. In the following tiny data set called `sbp_example`, we have two variables for a set of 10 subjects. The variables are named `sbp.before` and `sbp.after` and we are missing two values in the `sbp.before` data.

``` r
subject <- 101:110
x1 <- c(120, 145, 150, NA, 155, NA, 135, 160, 115, 170)
x2 <- c(105, 135, 150, 120, 135, 115, 160, 150, 130, 155)

sbp_example <- data.frame(id = subject, sbp.before = x1, sbp.after = x2)
sbp_example <- tbl_df(sbp_example)
sbp_example
```

    ## # A tibble: 10 x 3
    ##       id sbp.before sbp.after
    ##    <int>      <dbl>     <dbl>
    ##  1   101        120       105
    ##  2   102        145       135
    ##  3   103        150       150
    ##  4   104         NA       120
    ##  5   105        155       135
    ##  6   106         NA       115
    ##  7   107        135       160
    ##  8   108        160       150
    ##  9   109        115       130
    ## 10   110        170       155

Testing for Missing Values
--------------------------

The function `is.na(x)` returns TRUE if x is missing (NA). Applied to a variable, we get the following...

``` r
is.na(sbp_example$sbp.before)
```

    ##  [1] FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE

The importance of `na.rm` and other commands for omitting missing values
------------------------------------------------------------------------

If we summarize the data in the `sbp_example` tibble, we get warned that `sbp.before` has two missing values.

``` r
summary(sbp_example)
```

    ##        id          sbp.before      sbp.after    
    ##  Min.   :101.0   Min.   :115.0   Min.   :105.0  
    ##  1st Qu.:103.2   1st Qu.:131.2   1st Qu.:122.5  
    ##  Median :105.5   Median :147.5   Median :135.0  
    ##  Mean   :105.5   Mean   :143.8   Mean   :135.5  
    ##  3rd Qu.:107.8   3rd Qu.:156.2   3rd Qu.:150.0  
    ##  Max.   :110.0   Max.   :170.0   Max.   :160.0  
    ##                  NA's   :2

But if we try to run a mean of the `sbp.before` data, or a correlation between the `sbp.before` and `sbp.after` data, we need to tell R what to do about the missingness. Often, we'll use the `na.rm = TRUE` command within our function call to tell R to omit the cases with missing values. Some commands, like `cor`, in particular, don't take the `na.rm=TRUE` command, and instead we need to use a different command, like `use = "complete.obs"`. One thing that works for most situations is to use the `with(na.omit(datasetname), nameoffunctionyouwanttorun)` approach shown below.

``` r
mean(sbp_example$sbp.before)
```

    ## [1] NA

``` r
mean(sbp_example$sbp.before, na.rm = TRUE)
```

    ## [1] 143.75

``` r
with(na.omit(sbp_example), mean(sbp.before))
```

    ## [1] 143.75

``` r
cor(sbp_example$sbp.before, sbp_example$sbp.after)
```

    ## [1] NA

``` r
cor(sbp_example$sbp.before, sbp_example$sbp.after, use = "complete.obs")
```

    ## [1] 0.6286946

``` r
with(na.omit(sbp_example), cor(sbp.before, sbp.after))
```

    ## [1] 0.6286946

Using Simple Imputation (generally a bad plan)
----------------------------------------------

Suppose we want to do single imputation, and then run a scatterplot and correlation analysis to look at the linear association between `sbp.before` and `sbp.after`. Without imputation, we'd have the following.

### Results without imputing

``` r
ggplot(sbp_example, aes(x = sbp.before, y = sbp.after)) + 
  geom_point() +
  geom_smooth(method = "lm", col = "red") +
  labs(title = "Plot without Imputation (n = 8 subjects)")
```

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/run%20scatterplot%20and%20correlation%20analysis%20without%20imputation-1.png)

``` r
with(na.omit(sbp_example), cor(sbp.before, sbp.after))
```

    ## [1] 0.6286946

``` r
summary(lm(sbp.after ~ sbp.before, data = na.omit(sbp_example)))
```

    ## 
    ## Call:
    ## lm(formula = sbp.after ~ sbp.before, data = na.omit(sbp_example))
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -21.2319  -7.1739   0.1812   6.4493  25.0725 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept)  56.6667    42.4093   1.336    0.230  
    ## sbp.before    0.5797     0.2927   1.980    0.095 .
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 14.89 on 6 degrees of freedom
    ## Multiple R-squared:  0.3953, Adjusted R-squared:  0.2945 
    ## F-statistic: 3.922 on 1 and 6 DF,  p-value: 0.09499

### Simple Imputation using `mice`

We'll use the `mice` package to do the imputation, using a simple imputation to fill in the two missing `sbp.before` values and then rerun our plot and correlation analysis so as to include all 10 subjects.

``` r
library(mice)
```

    ## 
    ## Attaching package: 'mice'

    ## The following object is masked from 'package:tidyr':
    ## 
    ##     complete

``` r
md.pattern(sbp_example) 
```

    ##   id sbp.after sbp.before  
    ## 8  1         1          1 0
    ## 2  1         1          0 1
    ##    0         0          2 2

``` r
sbp.temp <- mice(sbp_example, m=1, maxit=50, meth='pmm', printFlag=FALSE, seed=431431)
completed.sbp <- complete(sbp.temp,1)
```

### Result after Simple Imputation

``` r
ggplot(completed.sbp, aes(x = sbp.before, y = sbp.after)) + 
  geom_point() +
  geom_smooth(method = "lm", col = "red") +
  labs(title = "Plot with Simple Imputation (n = 10 subjects)")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/run%20scatterplot%20and%20correlation%20analysis%20with%20simple%20imputation-1.png)

``` r
with(completed.sbp, cor(sbp.before, sbp.after))
```

    ## [1] 0.5404296

``` r
summary(lm(sbp.after ~ sbp.before, data = completed.sbp))
```

    ## 
    ## Call:
    ## lm(formula = sbp.after ~ sbp.before, data = completed.sbp)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -24.150  -8.250   2.122   8.022  28.570 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)  62.7419    40.3818   1.554    0.159
    ## sbp.before    0.5088     0.2801   1.817    0.107
    ## 
    ## Residual standard error: 16.35 on 8 degrees of freedom
    ## Multiple R-squared:  0.2921, Adjusted R-squared:  0.2036 
    ## F-statistic:   3.3 on 1 and 8 DF,  p-value: 0.1068

Using Multiple Imputation (generally a much better plan)
--------------------------------------------------------

Next, we'll use the `mice` package to do multiple imputation, and we'll run 100 imputations. In each, R will fill in the two missing `sbp.before` values, creating 100 new "completed" data sets.

``` r
md.pattern(sbp_example) 
```

    ##   id sbp.after sbp.before  
    ## 8  1         1          1 0
    ## 2  1         1          0 1
    ##    0         0          2 2

``` r
sbp.mi <- mice(sbp_example, m=100, maxit=5, meth='pmm', printFlag=FALSE, seed=43937)
```

### Linear Regression Model after Multiple Imputation

We can get a complete run on any single one of our imputed data sets. For instance, here's the result for imputation number 41.

``` r
imp41 <- complete(sbp.mi,41)

ggplot(imp41, aes(x = sbp.before, y = sbp.after)) + 
  geom_point() +
  geom_smooth(method = "lm", col = "red") +
  labs(title = "Plot with Imputation Number 41")
```

![](431_2017_working-with-data-in-R_files/figure-markdown_github-ascii_identifiers/regression%20model%20and%20correlation%20analysis%20using%20imputation%20number%2041-1.png)

``` r
with(imp41, cor(sbp.before, sbp.after))
```

    ## [1] 0.4550701

``` r
summary(lm(sbp.after ~ sbp.before, data = imp41))
```

    ## 
    ## Call:
    ## lm(formula = sbp.after ~ sbp.before, data = imp41)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -20.500 -15.176   3.389   8.574  29.315 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)  65.6852    48.6080   1.351    0.214
    ## sbp.before    0.4815     0.3331   1.445    0.186
    ## 
    ## Residual standard error: 17.31 on 8 degrees of freedom
    ## Multiple R-squared:  0.2071, Adjusted R-squared:  0.108 
    ## F-statistic: 2.089 on 1 and 8 DF,  p-value: 0.1863

### Looking at Pooled Regression Model Estimates

To get a set of pooled regression model estimates across all 100 imputations, we can do the following.

``` r
model1 <- with(sbp.mi, lm(sbp.after ~ sbp.before))
summary(pool(model1))
```

    ##                    est         se        t       df  Pr(>|t|)       lo 95
    ## (Intercept) 65.7706736 46.2980248 1.420594 5.718817 0.2075881 -48.8805210
    ## sbp.before   0.4883155  0.3224615 1.514337 5.596046 0.1842171  -0.3147337
    ##                  hi 95 nmis       fmi    lambda
    ## (Intercept) 180.421868   NA 0.3260978 0.1254963
    ## sbp.before    1.291365    2 0.3431956 0.1440446

### A Key Reference

-   We'll return to imputation in Parts B and (especially) C of the course.

-   If there are things you want to know about using MICE to do imputation work in R, check out van Buuren S Groothuis-Oudshoorn K (2011) at <https://stat.ethz.ch/education/semesters/ss2012/ams/paper/mice.pdf>

Additional Issues
=================

R ≠ R Studio ≠ R Markdown
-------------------------

1.  R is a statistical programming language that helps us solve problems.
2.  "We use R Studio because it makes us happier in our work." - Jenny Bryan
3.  We use R Markdown because we want to be able to reproduce our work.

We'll write R code, using R Studio, into R Markdown files.

Producing Word files instead of HTML
------------------------------------

Assuming you have Microsoft Office installed on your computer, you should be immediately able to write a Markdown file and render it in either HTML or as a Word document, by creating a Markdown document and then clicking on the little down arrow next to the Knit button at the top of R Studio and selecting either Knit HTML or Knit Word. In order to get Markdown to generate a PDF file directly, you have to install some additional software, as described below. To learn more about the various formatting options in R Markdown, visit <http://rmarkdown.rstudio.com/formats.html>

Generating a PDF using R Markdown
---------------------------------

To generate PDF (rather than Word or HTML) you'll want to download an installation of the TeX (TeX is pronounced \`\`tech'') software, which builds those relatively pretty documents. I use MacTeX on my Mac, and MikTeX on my PC. This also lets me include LaTeX and TeX commands directly within a Markdown file, which is something you might eventually want to do, and that I use when generating PDFs for this class.

-   If you want to be able to build PDF files from Markdown, you'll need to get the (free) software:
    -   <http://miktex.org/download> to get MiKTeX for the PC. There is a Tutorial on this page if you need step-by-step guidance.
    -   <https://tug.org/mactex/mactex-download.html> to get MacTeX for a Mac.
    -   On either the Mac or the PC, I would also consider downloading and installing TeXworks, which provides a nice front end if you're actually going to write things in LaTeX or TeX. Visit <https://www.tug.org/texworks/> and click **Get It**.

Once you've done this, you should be able to generate PDF files from R Markdown files within R Studio.
