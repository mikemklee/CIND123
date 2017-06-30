CIND123 - Lab 3
================

### Part 1.1 - Practice with charts

#### Creating a simple bar chart

``` r
# define vectors for Rating and Frequency
Rating <- c('A','B','C','D')
Frequency <- c(35,260,93,12)

# combine the vectors into a data frame
drawData <- data.frame(Rating,Frequency)

# draw a barchart
barplot(drawData$Frequency, names = drawData$Rating)
```

![](http://i.imgur.com/ZZPoQ0l.png)

#### Creating a pie chart

``` r
# Very basic pie chart
pChartData <- round(Frequency/sum(Frequency)*100)
pie(pChartData)
```

![](http://i.imgur.com/e4kFfqs.png)

``` r
# Pie Chart with Percentages
slices <- c(10, 12, 4, 16, 8) 
labels <- c("US", "UK", "Australia", "Germany", "France")
pct <- round(slices/sum(slices)*100)

# add percentages and symbol to labels 
labels <- paste(labels, pct)
labels <- paste(labels,"%",sep="")
pie(slices,labels = labels, col=rainbow(length(labels)),
    main="Pie Chart of Countries")
```

![](http://i.imgur.com/v7LaqSm.png)

#### Creating a line chart

``` r
# Line chart 1
# Specify type="o" for both points and lines
plot(Frequency,type = "o")
```

![](http://i.imgur.com/17Tzztd.png)

``` r
# Line chart 2
v <- c(7,12,28,3,41)
plot(v,type = "o", col = "blue", xlab = "Month", ylab = "Rain fall",
     main = "Rain fall chart")
```

![](http://i.imgur.com/R8e0hnD.png)

``` r
# Line chart 3
plot(v,type = "s", col = "green", xlab = "Month", ylab = "Rain fall",
     main = "Rain fall chart")
```

![](http://i.imgur.com/WWVnDPp.png)

#### Creating a stair step chart

``` r
# Generate some numbers and plot them using type='s'
plot(x <- sort(rnorm(47)), type = "s", main = "plot(x, type = \"s\")")

# Modify points design
points(x, cex = .5, col = "dark red")
```

![](http://i.imgur.com/T2TXvnc.png)

``` r
# Line chart 4
A <- c(2006,2011,2016,2021,2026,2031)
B <- c(1227.3, 1513.1, 1942.1, 2184.7, 2466.6, 2527.6)

plot(A,B,type = "o", main="Yearly Population Growth", xlab = "Year", ylab = "Population")
```

![](http://i.imgur.com/O5anw7c.png)

#### Creating a dot plot

``` r
# Generate a set of numbers
plot1 <- c(2,3,6,6,7,9)

# use dotchart() to draw a dot plot
dotchart(plot1)
```

![](http://i.imgur.com/nmmirok.png)

#### Creating a stem leaf diagram

``` r
# Generate a set of numbers
stem.leaf.plot <- c(90,70,70,70,75,70,65,68,60,74,70,95,75,70,68,65,40,65,70)

# stem() function to generate a stem leaf diagram
stem(stem.leaf.plot, scale = 2, width = 90)
```

    ## 
    ##   The decimal point is 1 digit(s) to the right of the |
    ## 
    ##   4 | 0
    ##   5 | 
    ##   6 | 055588
    ##   7 | 0000000455
    ##   8 | 
    ##   9 | 05

### Part 1.2 - Practice with GGPLOT2 and LATTICE packages

``` r
# Call in required packages
library(ggplot2)
library(lattice)
```

#### Creating a line chart

``` r
# Create a data frame with data
populationGrowth <- data.frame(
  year = c(2006, 2011, 2016, 2021, 2026, 2031),
  population = c(1227.3, 1513.1, 1942.1, 2184.7, 2466.6, 2527.6)
)

# Draw a line chart
ggplot(data=populationGrowth, aes(x=year, y=population, group=1)) +
  geom_line(colour="tomato", size=1.5) +
  geom_point(colour="tomato", size=4, shape=21, fill="white")
```

![](http://i.imgur.com/qdEkSW2.png)

#### Create a relative frequency histogram

``` r
# Create a vector of numbers
visitFrequency <- c(2, 6, 3, 3, 5, 7, 3, 4, 3, 4, 5, 8, 5, 3, 6)

# Draw a histogram
histogram(
  visitFrequency, 
  nint=7, 
  xlab="Visits", 
  ylab="Relative Frequency"
)
```

![](http://i.imgur.com/fSPJeWq.png)

### Part 2.1 - Exploring/cleaning a dataset

``` r
# Read in and create dataset with given CSV file
dataset <- read.csv("C:/Users/munky/Desktop/RU Bigdata/CIND123/Module 3/set1.csv", header=FALSE, stringsAsFactors=FALSE, na.strings=c("", "NA"))

# Attach headers for the columns
names(dataset) <- c("ID", "Fname", "Lname", "Email", "Gender", "Country", "Amount", "Date")

# Show summary of the dataset
summary(dataset)
```

    ##       ID               Fname              Lname          
    ##  Length:1000        Length:1000        Length:1000       
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character  
    ##     Email              Gender            Country         
    ##  Length:1000        Length:1000        Length:1000       
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character  
    ##     Amount              Date          
    ##  Length:1000        Length:1000       
    ##  Class :character   Class :character  
    ##  Mode  :character   Mode  :character

``` r
# Show number of countries without overlap
length(unique(dataset$Country))
```

    ## [1] 131

``` r
# Count number of Males, Females, and NA under the Gender column
sum(dataset$Gender == "Male", na.rm=TRUE)
```

    ## [1] 426

``` r
sum(dataset$Gender == "Female", na.rm=TRUE)
```

    ## [1] 471

``` r
sum(is.na(dataset$Gender))
```

    ## [1] 103

### Part 2.2 - Additional Practice

``` r
# Display a few clients who have NA as their country
head(dataset[is.na(dataset$Country),], n=3)
```

    ##            ID  Fname  Lname                Email Gender Country    Amount
    ## 28  68382-019 Joseph  Lynch                 <NA>   Male    <NA> $5,706.64
    ## 33  55315-519  Robin Taylor                 <NA> Female    <NA> $8,500.57
    ## 47 57955-0064  Kathy Graham kgraham1a@cpanel.net Female    <NA> $7,652.68
    ##          Date
    ## 28  4/22/2013
    ## 33 11/10/2011
    ## 47 11/23/2015

``` r
# Remove such clients
dataset <- dataset[!is.na(dataset$Country),]

# Remove the $ sign from Amount column and convert it to numeric
dataset$Amount <- as.numeric(gsub("[$,]", "", dataset$Amount))

# Convert Date column to data type date
dataset$Date <- as.Date(dataset$Date, "%m/%d/%y")

# Verify the results
head(dataset, n=3)
```

    ##          ID Fname Lname                  Email Gender  Country  Amount
    ## 1 0310-7820 Craig Welch                   <NA>   <NA> Mongolia 2527.52
    ## 2 41250-154  Judy   Kim     jkim1@buzzfeed.com Female Thailand 9004.47
    ## 3 59779-609 Jesse Smith jsmith2@shutterfly.com   Male    China 1445.94
    ##         Date
    ## 1 2020-07-11
    ## 2 2020-01-13
    ## 3 2020-01-29

``` r
# Identify earliest date and calculate number of days passed for each obvs. Insert into new column 'days'
dataset$days <- as.numeric(dataset$Date - min(dataset$Date))

# Create additional column 'IndEmail', where emails ending with 'gov' or 'org' get 1 and 0 for the rest
dataset$IndEmail <- 0
dataset$IndEmail[grep("gov", dataset$Email)] <- 1
dataset$IndEmail[grep("org", dataset$Email)] <- 1

# Verify the results
head(dataset, n=3)
```

    ##          ID Fname Lname                  Email Gender  Country  Amount
    ## 1 0310-7820 Craig Welch                   <NA>   <NA> Mongolia 2527.52
    ## 2 41250-154  Judy   Kim     jkim1@buzzfeed.com Female Thailand 9004.47
    ## 3 59779-609 Jesse Smith jsmith2@shutterfly.com   Male    China 1445.94
    ##         Date days IndEmail
    ## 1 2020-07-11  192        0
    ## 2 2020-01-13   12        0
    ## 3 2020-01-29   28        0
