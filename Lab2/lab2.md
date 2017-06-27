CIND123 - Lab 2
================

### Exercise 1

| RANK | PLAYER           | SALARY | YEARS |
|------|------------------|--------|-------|
| 1    | Jaromir Jagr     | 100    | 19    |
| 2    | Nicklas Lidstrom | 94     | 19    |
| 3    | Joe Sakic        | 87     | 20    |
| 4    | Mats Sundin      | 74     | 18    |
| 5    | Keith Tkachuk    | 74     | 17    |

The above data represents the salaries of the top 5 salaries in the NHL since 1989 rounded to the next million.

Create the data in each column in a new vector.

``` r
# Define each vector
rank <- c(1,2,3,4,5)
name <- c("Jaromir Jagr", "Nicklas Lidstrom", "Joe Sakic", "Mats Sundin", "Keith Tkachuk")
salary <- c(100, 94, 87, 74, 74)
active_years <- c(19, 19, 20, 18, 17)
```

Combine all vectors to create a matrix using cbind().

``` r
mat <- cbind(rank, name, salary, active_years)

# the complete matrix
mat
```

    ##      rank name               salary active_years
    ## [1,] "1"  "Jaromir Jagr"     "100"  "19"
    ## [2,] "2"  "Nicklas Lidstrom" "94"   "19"
    ## [3,] "3"  "Joe Sakic"        "87"   "20"
    ## [4,] "4"  "Mats Sundin"      "74"   "18"
    ## [5,] "5"  "Keith Tkachuk"    "74"   "17"

What is the salary of Joe Sakic?

``` r
mat[3,3]
```

    ## salary
    ##   "87"

How many year has Nicklas Lidstrom been active?

``` r
mat[2,4]
```

    ## active_years
    ##         "19"

Display all the player names.

``` r
mat[,2]
```

    ## [1] "Jaromir Jagr"     "Nicklas Lidstrom" "Joe Sakic"
    ## [4] "Mats Sundin"      "Keith Tkachuk"

### Exercise 2

The use of the c and sum functions.

This exercise uses epidemiological data. Vicente et al. (2006) analyzed data from observations of wild boar and red deer reared on a number of estates in Spain. The dataset contains information on tuberculosis (Tb) in both species, and on the parasite Elaphostrongylus cervi, which only infects red deer.

In Zuur et al. (2009), Tb was modelled as a function of the continuous explanatory variable, length of the animal, denoted by LengthCT (CT is an abbreviation of cabeza-tronco, which is Spanish for head-body). Tb and Ecervi are shown as a vector of zeros and ones representing absence or presence of Tb and E. cervi larvae.

Using the c function, create a variable that contains the length values of the first seven animals. Also create a variable that contains the Tb values. Include the NAs.

``` r
# Define vectors for the length and Tb values
length <- c(75, 85, 91.6, 95, NA, 105.5, 106)
tb <- c(0, 0, 1, NA, 0, 0, 1)
```

What is the average length of the seven animals?

``` r
# Display average length. Use 'na.rm=' parameter to remove NA values
mean(length, na.rm=TRUE)
```

    ## [1] 93.01667

### Exercise 3

The use of the cbind function using epidemiological data.

We continue with the deer from Exercise 2. First create variables Farm and Month that contain the relevant information. Note that Farm is a string of characters.

``` r
farm <- c("MO", "MO", "MO", "MO", "LN", "SE", "QM")
month <- c(11, 07, 07, NA, 09, 09, 11)
```

Use the cbind command to combine month, length, and Tb data, and store the results in the variable, Boar.

``` r
# Combine month, length, tb and store in boar
boar <- cbind(month, length, tb)
```

Make sure that you can extract rows, columns, and elements of Boar. Use the dim, nrow, and ncol functions to determine the number of animals and variables in Boar.

``` r
# Display dimension of boar matrix
dim(boar)
```

    ## [1] 7 3

``` r
# Display number of rows in boar
nrow(boar)
```

    ## [1] 7

``` r
# Display number of columns in boar
ncol(boar)
```

    ## [1] 3

### Exercise 4

Working with a matrix.

Create the following matrix in R and determine its transpose, its inverse, and multiply D with its inverse (the outcome should be the identity matrix).

|     |     |     |
|:----|:----|:----|
| 1   | 2   | 3   |
| 4   | 2   | 1   |
| 2   | 3   | 0   |

``` r
# Define values for matrix
d_values <- c(1, 2, 3, 4, 2, 1, 2, 3, 0)

# Define and display the matrix
d_matrix <- matrix(d_values, nrow=3, byrow=TRUE)
d_matrix
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    2    3
    ## [2,]    4    2    1
    ## [3,]    2    3    0

``` r
# Define and display the transpose of the matrix
d_matrix_trans <- t(d_matrix)
d_matrix_trans
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    4    2
    ## [2,]    2    2    3
    ## [3,]    3    1    0

``` r
# Define and display the inverse of the matrix
d_matrix_inv <- solve(d_matrix)
d_matrix_inv
```

    ##       [,1]  [,2]  [,3]
    ## [1,] -0.12  0.36 -0.16
    ## [2,]  0.08 -0.24  0.44
    ## [3,]  0.32  0.04 -0.24

``` r
# Calculate the product of the matrix and its inverse
d_matrix %*% d_matrix_inv
```

    ##              [,1] [,2] [,3]
    ## [1,] 1.000000e+00    0    0
    ## [2,] 5.551115e-17    1    0
    ## [3,] 0.000000e+00    0    1
