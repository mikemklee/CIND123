CIND123 - Lab 5
================

You are out in the market to buy a new car and you have found a list of all of the cars in the market.

``` r
auto_data <- read.table("C:/Users/munky/Desktop/RU Bigdata/CIND123/Module 5/Lab 5/auto-mpg.txt", na.strings="?")
```

First you want to get a feeling of the data. So you decide to look at the outputs of the summary function.

``` r
# Give each column a heading and then show summary
names(auto_data) <- c("mpg", 
                      "cylinders", 
                      "displacement", 
                      "horsepower", 
                      "weight", 
                      "acceleration", 
                      "model_yr", 
                      "origin", 
                      "car_name")

summary(auto_data)
```

    ##       mpg          cylinders      displacement     horsepower   
    ##  Min.   : 9.00   Min.   :3.000   Min.   : 68.0   Min.   : 46.0  
    ##  1st Qu.:17.50   1st Qu.:4.000   1st Qu.:104.2   1st Qu.: 75.0  
    ##  Median :23.00   Median :4.000   Median :148.5   Median : 93.5  
    ##  Mean   :23.51   Mean   :5.455   Mean   :193.4   Mean   :104.5  
    ##  3rd Qu.:29.00   3rd Qu.:8.000   3rd Qu.:262.0   3rd Qu.:126.0  
    ##  Max.   :46.60   Max.   :8.000   Max.   :455.0   Max.   :230.0  
    ##                                                  NA's   :6      
    ##      weight      acceleration      model_yr         origin     
    ##  Min.   :1613   Min.   : 8.00   Min.   :70.00   Min.   :1.000  
    ##  1st Qu.:2224   1st Qu.:13.82   1st Qu.:73.00   1st Qu.:1.000  
    ##  Median :2804   Median :15.50   Median :76.00   Median :1.000  
    ##  Mean   :2970   Mean   :15.57   Mean   :76.01   Mean   :1.573  
    ##  3rd Qu.:3608   3rd Qu.:17.18   3rd Qu.:79.00   3rd Qu.:2.000  
    ##  Max.   :5140   Max.   :24.80   Max.   :82.00   Max.   :3.000  
    ##                                                                
    ##            car_name  
    ##  ford pinto    :  6  
    ##  amc matador   :  5  
    ##  ford maverick :  5  
    ##  toyota corolla:  5  
    ##  amc gremlin   :  4  
    ##  amc hornet    :  4  
    ##  (Other)       :369

When you run the data, you see that the horse power column is classified as character.

-   Use the as.numeric() function to correct this column.

``` r
auto_data$horsepower <- as.numeric(as.character(auto_data$horsepower))
```

Now that all columns are numeric, you want to plot graphs to start your exploratory analysis.

Create a scatter plot using car weights in the x axis and acceleration in the y axis. (Use plot(x,y))

``` r
plot(auto_data$weight, auto_data$acceleration, type="p", xlab="Car Weights", ylab="Acceleration")
```

<img src="http://i.imgur.com/o9XFJw8.png" style="display: block; margin: auto 0 auto auto;" />

After your initial findings, you want to tackle your main issue; What car should you buy? You do not want to spend too much time for this pursuit. So, you have decided to introduce a rule based approach to narrow down the list to two cars. These rules are:

-   Pick the cars that have the median acceleration and find the lightest (in terms of weight) one.

-   Pick the car whose weight is closest to the mean.

**Guide for the rules:**

1.  You will have to use the which() function to access the indices of the cars with median acceleration. Then use which.min() to find the lightest car from the initial list. You will need to store two indices to access the car that match the rule's requirements.
2.  For the second rule, derive the difference between each car and the mean weight of the data set by using R's built-in mean function. Add these observations to the cars dataset.
3.  Then access the smallest value in the newly created column by using the which.min() function (You might need to use the absolute function before using the which.min() function).

``` r
# Find the index of car with median acceleration
median_ind <- which(auto_data$acceleration == median(auto_data$acceleration))

# Find the lightest car 
lightest_ind <- which.min(auto_data[median_ind,]$weight)

cat("Indices of cars with median acceleration are: ", median_ind, "\n\n")
```

    ## Indices of cars with median acceleration are:  16 17 31 35 36 37 38 58 115 119 121 141 143 148 151 183 211 220 250 312 319

``` r
cat("Within the above list, the index of the lighest car is: ", median_ind[lightest_ind], "\n\n")
```

    ## Within the above list, the index of the lighest car is:  143

``` r
auto_data$difference <- abs(auto_data$weight - mean(auto_data$weight))
closest_mean_ind <- which.min(auto_data$difference)

cat("The index of the car of which weight is closest to the mean is: ", closest_mean_ind)
```

    ## The index of the car of which weight is closest to the mean is:  255
