CIND123 - Lab 4
================

You have just begun an illustrious career in the real estate sector. You are given a large dataset containing every non-commercial property for sale in the city of Windsor for the past 6 months. It is your job to create functions to help interpret and make use of this data.

#### Question 1

Create a function that calculates the average of a set (without using R's mean() function). It should take a set of numbers as an input, and return the average.

``` r
# Define the function
calculate_avg <- function(number_set) {
  return (sum(number_set) / length(number_set))
}

# Define the test vector
vec <- c(1,3,5,7,9,11,13,15,17)

# Test the function
paste("The Mean is", calculate_avg(vec))
```

    ## [1] "The Mean is 9"

#### Question 2

Create a function that calculates Z scores. It should take in a single value, and a set of numbers as arguments, and return the Z-score. (Use the set of numbers to calculate the mean and standard deviation.)

``` r
# Define the function
calculate_z <- function(mean_val, number_set) {
  return ((mean_val - calculate_avg(number_set)) / sd(number_set))
}

# Define test variables
mean_value <- 30
numbers <- c(3,20,30,40,100,125)

# Test the function
paste("The z-score is", round(calculate_z(mean_value, numbers), digits=4))
```

    ## [1] "The z-score is -0.4759"

#### Question 3

Download Housing.csv. THere are no missing values in the dataset, and every element is numeric.

``` r
# Import the dataset
housing_data <- read.csv("C:/Users/munky/Desktop/RU Bigdata/CIND123/Module 4/Lab 4/housing.csv")
```

Clients frequently approach you with the maximum price they're willing to spend on a house. With this maximum price, create a function that returns 2 elements; the number of houses available at/below this price, and the portion of houses in the market that are at/below this price.

``` r
# Define the function
houses_available <- function(max_price) {
  num_houses <- sum(housing_data$price < max_price)
  prop_houses <- num_houses / length(housing_data$price)
  
  output <- list("Num. of houses available"=num_houses, "% of houses at/below this price"=prop_houses)
  return(output)
}

# Test the function
houses_available(70000)
```

    ## $`Num. of houses available`
    ## [1] 333
    ## 
    ## $`% of houses at/below this price`
    ## [1] 0.6098901

#### Question 4

Create a function that takes in a set of numbers and plots its histogram, and returns 1 if the set is skewed right, and -1 if it is skewed left. Use this function to plot and determine the skew of the prices.

``` r
# Define the function
skew <- function(num_set) {
  hist(num_set, breaks=10)
  if (mean(num_set) > median(num_set))
    return ("Data is skewed to the Right; 1")
  else
    return ("Data is skewed to the Left;-1")
}

# Define the test vector
vec2 <- rnorm(40, mean=50, sd=10)

# Test the function
skew(vec2)
```

<img src="http://i.imgur.com/n7ziK9u.png" style="display: block; margin: auto;" />

    ## [1] "Data is skewed to the Left;-1"

#### Question 5

Create a function that takes a price as an input, and returns the z-score of the average number of bedrooms for houses less than or equal to the inputted price. Also make it print a summary for the number of bath-pieces for houses at or below the inputted price.

``` r
# Define the function
bedroom_z <- function(input_price) {
  houses <- subset(housing_data, price <= input_price, select=price:bathrms)
  avg_bdr <- mean(houses$bedrooms)
  avg_all <- mean(housing_data$bedrooms)
  sd_all <- mean(housing_data$bedrooms)
  
  z_bdr <- (avg_bdr - avg_all) / sd_all
  
  print(summary(houses$bathrms))
  return (cat("The Z-score is: ", z_bdr))
}

# Test the function
bedroom_z(40000)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   1.000   1.000   1.000   1.075   1.000   3.000 
    ## The Z-score is:  -0.1473423

#### Question 6

Create a function that takes an upper price and a lower price as an argument, creates a subset of houses that fall into that interval, and returns the head of that subset.

``` r
# Define the function
houses_subset <- function(lower, upper) {
  houses <- subset(housing_data, lower <= price & price <= upper)
  head(houses)
}

# Test the function
houses_subset(35000, 75000)
```

    ##   price lotsize bedrooms bathrms stories driveway recroom fullbase gashw
    ## 1 42000    5850        3       1       2        1       0        1     0
    ## 2 38500    4000        2       1       1        1       0        0     0
    ## 3 49500    3060        3       1       1        1       0        0     0
    ## 4 60500    6650        3       1       2        1       1        0     0
    ## 5 61000    6360        2       1       1        1       0        0     0
    ## 6 66000    4160        3       1       1        1       1        1     0
    ##   airco garagepl prefarea
    ## 1     0        1        0
    ## 2     0        0        0
    ## 3     0        0        0
    ## 4     0        0        0
    ## 5     0        0        0
    ## 6     1        0        0

#### Question 7

Create a function that takes a number of bedrooms as input, and returns the cheapest house(s) with that number of bedrooms.

``` r
# Define the function
cheap_house <- function(bedroom_num) {
  houses <- subset(housing_data, bedrooms == bedroom_num)
  cheapest <- houses[which(houses$price == min(houses$price)),]
  return (cheapest)
}

# Test the function
cheap_house(3)
```

    ##     price lotsize bedrooms bathrms stories driveway recroom fullbase gashw
    ## 163 25000    2910        3       1       1        0       0        0     0
    ## 233 25000    3850        3       1       2        1       0        0     0
    ##     airco garagepl prefarea
    ## 163     0        0        0
    ## 233     0        0        0
