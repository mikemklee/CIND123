CIND123 - Lab 9
================

### Part 1 - Sampling Distribution

-   Create a vector \[5, 10 15\]
-   Load the gtools library
-   Use the premutations function in gtools to list all possible outcomes when 2 numbers are selected with replacement. Hint: Set the argument repeats.allowed =TRUE in the premutations function
-   Use the rowMeans() function to calculate the mean of each possible pair of outcomes
-   Is the mean of the original population == the mean of the row means?
-   Use the hist() function to draw a histogram of the pairs' means

``` r
my_vec <- c(5, 10, 15)
library(gtools)

perm_result <- permutations(n=3, r=2, v=my_vec, repeats.allowed = TRUE)

row_means <- rowMeans(perm_result)

# mean of row means
mean(row_means)
```

    ## [1] 10

``` r
# mean of original population
mean(my_vec)
```

    ## [1] 10

``` r
hist(row_means)
```

![](http://i.imgur.com/wJBZntB.png)

### Part 2 - Central Limit Theorem

``` r
sdm.sim <- function(n, src.dist=NULL, param1=NULL, param2=NULL) {
  r <- 10000 # Number of replications/samples
  # This produces a matrix of observations with n columns and r rows.
  # Each row is one sample
  my.samples <- switch(src.dist,
                       "N"= matrix(rnorm(n*r, param1, param2), r),
                       "P"= matrix(rpois(n*r, param1), r))
  all.sample.sums <- apply(my.samples, 1, sum)
  all.sample.means <- apply(my.samples, 1, mean)
  all.sample.vars <- apply(my.samples, 1, var)
  
  par(mfrow=c(2,2))
  par(mar=c(1,1,1,1))
  opar=par(ps=6) # Make text 18 point
  hist(my.samples[1,], col="gray", main="Distribution of One Sample")
  hist(all.sample.sums, col="gray", main="Sampling Distribution of the Sum", ps=10)
  hist(all.sample.means, col="gray", main="Sampling Distribution of the Mean", ps=10)
  hist(all.sample.vars, col="gray", main="Sampling Distribution of the Variance", cex=0.8)
}

# Test function
sdm.sim(5, src.dist = "N", param1 = 20, param2 = 3)
```

![](http://i.imgur.com/0zUxhZs.png)

### Part 3 - Convergence of Poisson and Binomial Distribution to Normal Distribution

``` r
# When the sample set is large, Poisson distribution with lambda n converges to Normal distribution with mean n and variance n.

# Normal Distribution
sdm.sim(1000, src.dist = "N", param1=5, param2=5)
```

![](http://i.imgur.com/js5KBXO.png)

``` r
# Poisson Distribution
sdm.sim(1000, src.dist = "P", param1=5)
```

![](http://i.imgur.com/W34UyWz.png)
