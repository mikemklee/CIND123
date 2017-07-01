CIND123 - Lab 6
================

### Part 1 - Binomal Distribution

#### Question 1

Investigate the probability distribution of coin tosses and find the probability of getting cerntain outcomes.

``` r
# Simulate 10000 tosses and draw a histogram
x <- rbinom(10000,5,0.5)
hist(x)
```

![](http://i.imgur.com/Tu0aFjk.png)

``` r
# Simulate 10 random tosses and draw a histogram
y <- rbinom(10,5,0.5)
hist(y)
```

![](http://i.imgur.com/TJ8Ecie.png)

``` r
# Find the probability of getting at least 4 heads
dbinom(4,5,0.2)
```

    ## [1] 0.0064

``` r
# Estimate at least 4 heads
mean(x >= 4)
```

    ## [1] 0.1803

#### Question 2

What is the probability of having 2 successes for a random variable X with a distribution of Binomial(6, 1/3)

-   Binomial(n,p) corresponds to a binomial distribution with n independent Bernoulli trials where probability of success is p.

-   Investigate the function choose() try to calculate the same probability using the choose function.

``` r
# Calculation using dbinom()
dbinom(2,6,1/3)
```

    ## [1] 0.3292181

``` r
# Calculation using choose()
choose(6,2)*(1/3)^2*(2/3)^4
```

    ## [1] 0.3292181

#### Question 3

Compute the whole sample space for a random variable X with a distribution of Binomial(9, 3/4).

``` r
dbinom(0:9,9,3/4)
```

    ##  [1] 3.814697e-06 1.029968e-04 1.235962e-03 8.651733e-03 3.893280e-02
    ##  [6] 1.167984e-01 2.335968e-01 3.003387e-01 2.252541e-01 7.508469e-02

#### Question 4

For a disease known to have a complication frequency of 20%, a surgeon suggests a new procedure. He tests it on 10 patients and there are no complications. What is the probability of operating on 10 patients successfully with the traditional method?

``` r
dbinom(0, size=10, prob=.2)
```

    ## [1] 0.1073742

#### Question 5

Suppose there are twelve multiple choice questions in an English class quiz. Each question has five possible answers, and only one of them is correct. Find the probability of having four or less correct answers if a student attempts to answer every question at random.

``` r
pbinom(4, size=12, prob=0.2)
```

    ## [1] 0.9274445

### Part 2 - Poisson Distribution

If there are twelve cars crossing a bridge per minute on average, find the probability of having seventeen or more cars crossing the bridge in a particular minute.

-   Calculate the probability of having sixteen or less cars crossing the bridge in a particular minute.

``` r
# The probability of having sixteen or less cars crossing the bridge in a particular minute is given by the function ppois.

# Lower tail
ppois(16, lambda=12)
```

    ## [1] 0.898709

``` r
# Hence the probability of having seventeen or more cars crossing the bridge in a minute is in the upper tail of the probability density function. 

# Upper tail
ppois(16, lambda=12, lower=FALSE)
```

    ## [1] 0.101291

``` r
# The probability of having seventeen or more cars crossing the bridge for any given minute is 10.1%"
```

### Part 3 - Hypergeometric Distribution

We are working at a forest conservation agency and our task is to tag a population of endangered deer to prevent illegal hunting. We know that the forest has approximately 400 deer. Last week, we have captured 100 of the deer and tagged, and released them into the wild. This week we have captured 125 deer. What is the probability that we have captured 30 deer that were captured last week. (Assume that the recaptured deer are equally likely to be caught and they do not learn to avoid humans)

``` r
choose(100,30) * choose(300,95)/choose(400,125)
```

    ## [1] 0.09507884

``` r
# We have 100 successes, we want to get 30 of those "successes". 

# We have 95 failures, we want to get those from rest of the population. 

# We then divide by the total of different choices we can have 
dhyper(30, 100, 300, 125)
```

    ## [1] 0.09507884
