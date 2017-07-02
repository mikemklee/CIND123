CIND123 - Lab 8
================

### Exploring Normal Distribution

#### Question 1

Generate a sample of size 100 from a standard normal distribution.

``` r
A <- rnorm(100)
mean(A)
```

    ## [1] 0.003535924

``` r
sd(A)
```

    ## [1] 0.9067124

Generate a sample of size 100 with mean=2 and sd=5

``` r
B <- rnorm(100, mean=2, sd=5)
mean(B)
```

    ## [1] 1.225675

``` r
sd(B)
```

    ## [1] 4.85531

Find the height of the normal distribution for z=1.96

``` r
dnorm(1.96)
```

    ## [1] 0.05844094

#### Question 2

Assume that the test scores of a college entrance exam fits a normal distribution.

Furthermore, the mean test score is 62, and the standard deviation is 14.2.

What is the percentage of students scoring 86 or more in the exam?

``` r
1 - pnorm(86, mean=62, sd=14.2)
```

    ## [1] 0.04550051

#### Question 3

Joseph and Muhammed often travel to Ryerson University from their job in Mississauga.

Muhammed tends to drive from the highway, so his arrival to the University has a Normal distribution with a mean of 30 minutes and a standard deviation 3 minutes.

Joseph tends to prefer side roads so he sometimes get stuck behind school buses but makes up for the lost time by driving faster. His arrival time has a normal distribution with a mean of 27 minutes with a standard deviation of 7 minutes.

Their travel times are independent from each other.

On Joseph's probability distribution curve, find the height of the curve, in case arriving in 28.5 minutes.

``` r
dnorm(28.5, mean=27, sd=7)
```

    ## [1] 0.05569818

How does Joseph's arrival time distribution look like, plot the period from 15 to 45 minutes?

``` r
curve(dnorm(x, mean=27, sd=7), from=15 , to=45 )
```

![](http://i.imgur.com/YxKE0Kn.png)

Create a normally distributed sample set for Joseph with a size of 200. Plot a histogram for this dataset.

``` r
set.seed(25)
joseph <- rnorm(200, mean=27, sd=7)
hist(joseph, breaks=15)
```

![](http://i.imgur.com/SfDi1NX.png)

Find Muhammed's arrival time corresponding to the 80th percentile (i.e., what is the time of arrivalcorresponding to 80% of times?).

``` r
qnorm(0.8, mean=30, sd=3)
```

    ## [1] 32.52486

Find the probability that Joseph arrives to the University in 20 minutes or less.

``` r
pnorm(20, mean=27, sd=7)
```

    ## [1] 0.1586553

Find the probability for 1min, 5min, 10min, and 15min or less

``` r
pnorm(1, mean=27, sd=7)
```

    ## [1] 0.0001018892

``` r
pnorm(5, mean=27, sd=7)
```

    ## [1] 0.0008365374

``` r
pnorm(10, mean=27, sd=7)
```

    ## [1] 0.007579219

``` r
pnorm(15, mean=27, sd=7)
```

    ## [1] 0.04323813
