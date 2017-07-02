CIND123 - Lab 10
================

Running linear regressions on R
-------------------------------

### Part 1 - Cats

``` r
library(MASS)
data(cats)
attach(cats)
```

The data set includes 3 variables: Sex, Body weight (kg) and heart weight (g). These variable can be found with the st r() function.

Create a linear model where heart weight is the dependent variable and body weight is the independent variable. What is the intercept and the slope of this model? How can you interpret the slope of this model?

``` r
simple_model <- lm(Hwt ~ Bwt)
# intercept: -0.3567
# slope: 4.0341
# one unit increase in body weight is associated with 4.0341 units increase in heart weight
```

Now draw a scatter plot with this data and insert this linear model into it. (Hint: abline() ). Try to distinguish the sex of the cats in the scatter plot by using the points() function.

``` r
plot(Bwt, Hwt, 
     pch = 15, 
     cex = 0.7, 
     main = "Body weight vs. Heart weight", 
     xlab = "Body Weight", 
     ylab = "Heart Weight",
     col=ifelse(Sex=="M", "black", 
                ifelse(Sex=="F", "pink", "black")
                )
     )
abline(simple_model)
```

![](http://i.imgur.com/nTffGYn.png)

Predict the heart weight of a cat that is 3.5 kilograms. Can you accurately predict the heart weight of a cat that is 6.5 kilograms?

``` r
newData <- data.frame(Bwt=3.5)
predict(simple_model, newData, interval="predict")
```

    ##        fit      lwr      upr
    ## 1 13.76256 10.85605 16.66907

``` r
newData2 <- data.frame(Bwt=6.5)
predict(simple_model, newData2, interval="predict")
```

    ##        fit      lwr     upr
    ## 1 25.86475 22.43099 29.2985

``` r
detach(cats)
```

### Part 2 - Mtcars

First, model the mpg variable on hp and then model the mpg variable on wt. Check the summary command for both of the models.

``` r
attach(mtcars)

model1 <- lm(mpg ~ hp)
model2 <- lm(mpg ~ wt)

summary(model1)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ hp)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -5.7121 -2.1122 -0.8854  1.5819  8.2360 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 30.09886    1.63392  18.421  < 2e-16 ***
    ## hp          -0.06823    0.01012  -6.742 1.79e-07 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.863 on 30 degrees of freedom
    ## Multiple R-squared:  0.6024, Adjusted R-squared:  0.5892 
    ## F-statistic: 45.46 on 1 and 30 DF,  p-value: 1.788e-07

``` r
summary(model2)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ wt)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.5432 -2.3647 -0.1252  1.4096  6.8727 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  37.2851     1.8776  19.858  < 2e-16 ***
    ## wt           -5.3445     0.5591  -9.559 1.29e-10 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.046 on 30 degrees of freedom
    ## Multiple R-squared:  0.7528, Adjusted R-squared:  0.7446 
    ## F-statistic: 91.38 on 1 and 30 DF,  p-value: 1.294e-10

``` r
detach(mtcars)
```

### Part 3 - Wage

``` r
library(ISLR)
attach(Wage)
```

Explore the variables of the dataset using str() or with ?Wage. Build a regression model where wage is the dependent variable and age, job class (which has 1 for Industrial and 2 for Information) and education are the independent variable.

How can we interpret the slope of age? Keep in mind that this definition will be slightly different then the previous ones as we have multiple variables in the model.

``` r
str(Wage)
```

    ## 'data.frame':    3000 obs. of  12 variables:
    ##  $ year      : int  2006 2004 2003 2003 2005 2008 2009 2008 2006 2004 ...
    ##  $ age       : int  18 24 45 43 50 54 44 30 41 52 ...
    ##  $ sex       : Factor w/ 2 levels "1. Male","2. Female": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ maritl    : Factor w/ 5 levels "1. Never Married",..: 1 1 2 2 4 2 2 1 1 2 ...
    ##  $ race      : Factor w/ 4 levels "1. White","2. Black",..: 1 1 1 3 1 1 4 3 2 1 ...
    ##  $ education : Factor w/ 5 levels "1. < HS Grad",..: 1 4 3 4 2 4 3 3 3 2 ...
    ##  $ region    : Factor w/ 9 levels "1. New England",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ jobclass  : Factor w/ 2 levels "1. Industrial",..: 1 2 1 2 2 2 1 2 2 2 ...
    ##  $ health    : Factor w/ 2 levels "1. <=Good","2. >=Very Good": 1 2 1 2 1 2 2 1 2 2 ...
    ##  $ health_ins: Factor w/ 2 levels "1. Yes","2. No": 2 2 1 1 1 1 1 1 1 1 ...
    ##  $ logwage   : num  4.32 4.26 4.88 5.04 4.32 ...
    ##  $ wage      : num  75 70.5 131 154.7 75 ...

``` r
wage_model <- lm(wage ~ age + jobclass + education)

summary(wage_model)
```

    ## 
    ## Call:
    ## lm(formula = wage ~ age + jobclass + education)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -106.656  -20.043   -3.488   14.908  217.504 
    ## 
    ## Coefficients:
    ##                             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                 59.58000    3.24874  18.339  < 2e-16 ***
    ## age                          0.55537    0.05725   9.701  < 2e-16 ***
    ## jobclass2. Information       4.51067    1.38091   3.266   0.0011 ** 
    ## education2. HS Grad         11.20088    2.47733   4.521 6.38e-06 ***
    ## education3. Some College    23.33036    2.61811   8.911  < 2e-16 ***
    ## education4. College Grad    38.38622    2.62045  14.649  < 2e-16 ***
    ## education5. Advanced Degree 62.91152    2.87492  21.883  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 35.89 on 2993 degrees of freedom
    ## Multiple R-squared:  0.2619, Adjusted R-squared:  0.2605 
    ## F-statistic:   177 on 6 and 2993 DF,  p-value: < 2.2e-16

``` r
detach(Wage)
```

### Part 4 - Hsb

Build a linear regression model for the response variable "science". Use all the other variables in the dataset as independent variables.

``` r
library(faraway)
attach(hsb)
str(hsb)
```

    ## 'data.frame':    200 obs. of  11 variables:
    ##  $ id     : int  70 121 86 141 172 113 50 11 84 48 ...
    ##  $ gender : Factor w/ 2 levels "female","male": 2 1 2 2 2 2 2 2 2 2 ...
    ##  $ race   : Factor w/ 4 levels "african-amer",..: 4 4 4 4 4 4 1 3 4 1 ...
    ##  $ ses    : Factor w/ 3 levels "high","low","middle": 2 3 1 1 3 3 3 3 3 3 ...
    ##  $ schtyp : Factor w/ 2 levels "private","public": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ prog   : Factor w/ 3 levels "academic","general",..: 2 3 2 3 1 1 2 1 2 1 ...
    ##  $ read   : int  57 68 44 63 47 44 50 34 63 57 ...
    ##  $ write  : int  52 59 33 44 52 52 59 46 57 55 ...
    ##  $ math   : int  41 53 54 47 57 51 42 45 54 52 ...
    ##  $ science: int  47 63 58 53 53 63 53 39 58 50 ...
    ##  $ socst  : int  57 61 31 56 61 61 61 36 51 51 ...

``` r
science_model <- lm(science ~ ., data=hsb)

summary(science_model)
```

    ## 
    ## Call:
    ## lm(formula = science ~ ., data = hsb)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -17.1123  -4.1821  -0.1337   3.7360  20.3646 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  -2.82445    4.77247  -0.592 0.554693    
    ## id            0.03203    0.01761   1.818 0.070611 .  
    ## gendermale    2.76996    1.03407   2.679 0.008057 ** 
    ## raceasian     1.65538    2.60596   0.635 0.526064    
    ## racehispanic  3.39705    2.07452   1.638 0.103223    
    ## racewhite     2.71877    2.16839   1.254 0.211489    
    ## seslow       -1.41171    1.43893  -0.981 0.327831    
    ## sesmiddle    -0.67689    1.13200  -0.598 0.550600    
    ## schtyppublic  2.60124    1.71611   1.516 0.131282    
    ## proggeneral   4.15481    1.25944   3.299 0.001164 ** 
    ## progvocation  2.12559    1.36456   1.558 0.121011    
    ## read          0.28654    0.07173   3.995 9.33e-05 ***
    ## write         0.30087    0.07608   3.955 0.000109 ***
    ## math          0.29137    0.07569   3.849 0.000163 ***
    ## socst        -0.02779    0.06308  -0.440 0.660105    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 6.51 on 185 degrees of freedom
    ## Multiple R-squared:  0.5981, Adjusted R-squared:  0.5677 
    ## F-statistic: 19.66 on 14 and 185 DF,  p-value: < 2.2e-16

``` r
detach(hsb)
```
