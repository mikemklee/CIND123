CIND123 - Lab 11
================

Exploring correlations in R
---------------------------

### Question 1

Load the data set height\_selfesteem.csv

1.  Identify the variables and find the correlation between height and self-esteem. What kind of relationship do these variables have?

2.  Based on the strength of the correlation, can we conclude there is a causal relationship between the two variables? Why or why not?

3.  Find the covariance of these variables. What is the relationship between covariance and correlation? How do they differ?

``` r
ht_self <- read.csv("C:/Users/munky/Desktop/RU Bigdata/CIND123/Module 11/height_selfesteem.csv")

cor(ht_self$Height, ht_self$Self.Esteem)
```

    ## [1] 0.7306357

``` r
# corr= 0.73 indicates strong positive correlation

cov(ht_self$Height, ht_self$Self.Esteem)
```

    ## [1] 1.371579

### Question 2

Load the dataset mtcars (exists in R: hint: attach(mtcars))

Test the correlation between mpg and weight variables.

-   What is the default method for cor.test()?

-   How you will interpret the output of this test?

``` r
attach(mtcars)

# test correlation between mpg and weight
cor.test(mpg, wt, method="pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  mpg and wt
    ## t = -9.559, df = 30, p-value = 1.294e-10
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.9338264 -0.7440872
    ## sample estimates:
    ##        cor 
    ## -0.8676594

``` r
# default method is pearson

# t is the t-test statistic value (t = -9.559),
# df is the degrees of freedom (df= 30),
# p-value is the significance level of the t-test (p-value = 1.29410^{-10}).
# conf.int is the confidence interval of the correlation coefficient at 95% (conf.int = [-0.9338, -0.7441]);
# sample estimates is the correlation coefficient (Cor.coeff = -0.87).
# The p-value of the test is 1.29410^{-10}, 
# which is less than the significance level alpha = 0.05. 
# We can conclude that wt and mpg are significantly correlated with a correlation 
# coefficient of -0.87 and p-value of 1.29410^{-10} .
```

Test the correlation between number of cylinders (cyl) and horsepower (hp). Is it a significant relationship?

Test the correlation between number of carburetors (carb) and gear (gear). Is it a significant relationship?

``` r
# test correlation between num of cylinders and horsepower
cor.test(cyl, hp)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  cyl and hp
    ## t = 8.2286, df = 30, p-value = 3.478e-09
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.6816016 0.9154223
    ## sample estimates:
    ##       cor 
    ## 0.8324475

``` r
# test correlation between num of carburetors and gear
cor.test(carb, gear)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  carb and gear
    ## t = 1.5609, df = 30, p-value = 0.129
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.08250603  0.56844218
    ## sample estimates:
    ##       cor 
    ## 0.2740728

Create a scatterplot matrix consisting of variables horsepower, cylinder and displacement. Do you see any patterns?

``` r
# scatterplot matrix consisting of horsepower, cylinder and displacement
my_var <- c("disp", "hp", "cyl")
pairs(mtcars[my_var])
```

![](http://i.imgur.com/orrDeS0.png)

Explore the corrgram package.

``` r
library(corrgram)
```

    ## Warning: package 'corrgram' was built under R version 3.3.3

``` r
corrgram(mtcars, order=TRUE, lower.panel=panel.shade,
         upper.panel=panel.pie, text.panel=panel.txt,
         main="Car Milage Data in PC2/PC1 Order")
```

![](http://i.imgur.com/YJNIqbZ.png)

### Question 4

We have a small dataset of Tourists in Toronto from different countries that includes the gender, number of children and how much they spent in CAD during the visit. We are interested to find out if tourists with greater numbers of children spend more.

-   Load the data set toursit.csv

-   Calculate the correlation between CHILDREN and SPEND and analyze the result

``` r
tourist <- read.csv("C:/Users/munky/Desktop/RU Bigdata/CIND123/Module 11/tourist.csv") 

# calculate correlation between CHILDREN and SPEND
attach(tourist)
cor(CHILDREN, SPEND)
```

    ## [1] -0.2612796

``` r
# cor = -0.2612796, weak correlation, and it is negative.
# This means tourists with a greater number of children tend to spend less!
```

-   Turn CHILDREN into a factor, using as.factor() to see how many levels it has.

-   As you can see, CHILDREN is a discrete variable without many values, so a Spearman correlation can be a better option. Run correlation test between CHILDREN and SPEND based on Spearman method.

-   How do you interpret this result?

``` r
# turn CHILDREN into factor to see how many level it has
levels(as.factor(CHILDREN))
```

    ## [1] "0" "1" "2" "3" "4" "5"

``` r
# Run correlation test with spearman method
cor.test(CHILDREN, SPEND, method ="spearman")
```

    ## Warning in cor.test.default(CHILDREN, SPEND, method = "spearman"): Cannot
    ## compute exact p-value with ties

    ## 
    ##  Spearman's rank correlation rho
    ## 
    ## data:  CHILDREN and SPEND
    ## S = 3016.9, p-value = 0.1382
    ## alternative hypothesis: true rho is not equal to 0
    ## sample estimates:
    ##        rho 
    ## -0.3116905

``` r
# cor = -0.3116905
#We have obtained a similar but slightly different correlation coefficient estimate because the Spearman correlation is indeed calculated differently than the Pearson.
```
