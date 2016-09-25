---
title: "R Cheat Sheet"
description: "R Cheat Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---


# Table of contents

* TOC
{:toc}

# Preliminaries
```R
library(tidyr)
library(dplyr)
```

(<a href="#top">Back to top</a>)
<hr>

# Input / Output

## Read

### CSV
```R
train <- read.csv("../train.csv", stringsAsFactors = F, row.names = 1)
# Column headers are values, not variable names
pew <- tbl_df(read.csv("pew.csv", stringsAsFactors = FALSE, check.names = FALSE))
```

```R
pew
#> # A tibble: 18 x 11
#>                   religion `<$10k` `$10-20k` `$20-30k` `$30-40k` `$40-50k`
#>                      <chr>   <int>     <int>     <int>     <int>     <int>
#> 1                 Agnostic      27        34        60        81        76
#> 2                  Atheist      12        27        37        52        35
#> 3                 Buddhist      27        21        30        34        33
```

```R
# using read.table
uciCar <- read.table( 'http://www.win-vector.com/dfiles/car.data.csv', sep=',',	header=T)
```

(<a href="#top">Back to top</a>)
<hr>

### JSON
```R
library("rjson")
json_data <- fromJSON(file=json_file)
# or
library(jsonlite)
winners <- fromJSON("winners.json", flatten=TRUE)

```


### As function 
```R
ss <- sample.submission()
#.. later
sample.submission <- function(){
  # Loads the sample submission, which is used in writing predictions
  ss <- read.csv(paste0(paths$data, 'sampleSubmission.csv'))
}
```

(<a href="#top">Back to top</a>)
<hr>

### Custom headers
```R
raw.train <- function(){
  # Loads the training data with correct classes
  cls <- c('factor', 'factor', 'Date', 'numeric', 'logical')
  train <- read.csv(paste0(paths$data, 'train.csv'), 
                    colClasses=cls)
}
```
(<a href="#top">Back to top</a>)
<hr>


### Generate Testdata
```R
set.seed(10)
messy <- data.frame(
  id = 1:4,
  trt = sample(rep(c('control', 'treatment'), each = 2)),
  work.T1 = runif(4),
  home.T1 = runif(4),
  work.T2 = runif(4),
  home.T2 = runif(4)
)
```

gives

```R
  id       trt    work.T1   home.T1   work.T2    home.T2
1  1 treatment 0.08513597 0.6158293 0.1135090 0.05190332
2  2   control 0.22543662 0.4296715 0.5959253 0.26417767
3  3 treatment 0.27453052 0.6516557 0.3580500 0.39879073
4  4   control 0.27230507 0.5677378 0.4288094 0.83613414
```

(<a href="#top">Back to top</a>)
<hr>

## Write

### Terminal
```R
cat("simplifying names...\n")
print(paste('dept:', d))
```

(<a href="#top">Back to top</a>)
<hr>

### File
```R
write.csv(ss, file = "/directoryname/filename.csv", quote=FALSE, row.names=FALSE)
```

(<a href="#top">Back to top</a>)
<hr>

## Define paths

```R
paths = list(data='../data/',
             submit='../submissions/',
             r='../R/')
.. later
paths$data             
```

(<a href="#top">Back to top</a>)
<hr>

# Whole DataFrame
[dplyr tutorial](http://rpubs.com/justmarkham/dplyr-tutorial)

## Content / Structure
```R
head(train[, -c(1, 5)])
head(mydata, n = 20) # first 20 rows to console
View(mydata)         # spreadsheet view 
tail(mydata)     # prints the last few rows
str(train)             # "str" stands for structure
class(train)         # gets class
dim(writers_df) # check dimensions
names(df)
sapply(ds,class)
attributes(df)    # list of values per variable
rownames(mydata) # view row names (numbers, if you haven't assigned names)
is.data.frame(mydata)           # TRUE or FALSE
ncol(mydata)                    # number of columns in data frame
nrow(mydata)                    # number of rows
names(mydata)                   # variable names
rownames(mydata)                # optional row names
```


```R
library(dplyr)
glimpse(data)
```

(<a href="#top">Back to top</a>)
<hr>

## Select

### Single or Multiple conditions

```R
mydata[mydata$sex == "f" & mydata$size.mm > 25, c("site","id","weight")]
```

```R
newdata <- subset(mydata, sex == "f" & size.mm > 25, select = c(site,id,weight))
# or
custdata2 <- subset(custdata,   (custdata$age > 0 & custdata$age < 100   & custdata$income > 0))
```

## SQL
```R
library(sqldf)
newdf <- sqldf("select * from mtcars where carb=1 order by mpg",
                  row.names=TRUE)
newdf
```

# Summary

## by index,name

```R
df$site        # the site vector
df$quadrat     # the quadrat vector
df[,]               # All Rows and All Columns
df[1,]              # First row and all columns
df[1:2,]            # First two rows and all columns
df[ c(1,3), ]       # First and third row and all columns
df[1, 2:3]          # First Row and 2nd and third column
df["Mazda RX4", "cyl"] # Row and column name
df[1:2, 2:3]        # First, Second Row and Second and Third COlumn
df[, 1]             # Just First Column with All rows
df[,c(1,3)]         # First and Third Column with All rows
#
df[1:4, c("Name", "Surname")]
```

(<a href="#top">Back to top</a>)
<hr>

### Summarize data

```R
dplyr::summarise(iris, avg = mean(Sepal.Length))  # Summarise data into single row of values. dplyr::summarise_each(iris, funs(mean))# Apply summary function to each column.dplyr::count(iris, Species, wt = Sepal.Length) # Count number of rows with each unique value ofvariable (with or without weights).
```

(<a href="#top">Back to top</a>)
<hr>

## Summary function

```R
dplyr::first   # First value of a vector.dplyr::last   # Last value of a vector.dplyr::nth    # Nth value of a vector.dplyr::n       # of values in a vector.dplyr::n_distinct   # of distinct values i
min   #Minimum value in a vector.max  # Maximum value in a vector.mean  # Mean value of a vector.median  # Median value of a vector.var    # Variance of a vector.sd    # Standard deviation of a vector
```
(<a href="#top">Back to top</a>)
<hr>



# Columns

## Info

### Type of Column
```R
sapply(df[ , !nums], class)
```

## Selecting

### by name

```R
mydata$site        # the site vector
mydata$quadrat     # the quadrat vector
```

### only numeric features

```R
nums <- sapply(x, is.numeric)
# Then standard subsetting
x[ , nums]
```

(<a href="#top">Back to top</a>)
<hr>


## Changing

## Manipulating

### Change column names
```R
names(mydata)[1] <- c("quad")   # change 1st variable name to quad
```

### Add columns
```R
dplyr::mutate(iris, sepal = Sepal.Length + Sepal. Width) # Compute and append one or more new columns.dplyr::mutate_each(iris, funs(min_rank))   # Apply window function to each column.dplyr::transmute(iris, sepal = Sepal.Length + Sepal. Width) # Compute one or more new columns. Drop original columns.
mydata$meanx <- (mydata$x1 + mydata$x2)/2
```

log-transform

```R
mydata$logsize <- log(mydata$size.mm)
```

(<a href="#top">Back to top</a>)
<hr>

### Window function
```R
dplyr::lead # Copy with values shi ed by 1.dplyr::lag   # Copy with values lagged by 1.dplyr::dense_rank # Ranks with no gaps.dplyr::min_rank  # Ranks. Ties get min rank.dplyr::percent_rank # Ranks rescaled to [0, 1].dplyr::row_number  # Ranks. Ties got to first value.dplyr::ntile  # Bin vector into n buckets.dplyr::between  # Are values between a and b?dplyr::cume_dist # Cumulative distribution.dplyr::cumall # Cumulative alldplyr::cumany # Cumulative anydplyr::cummean # Cumulative meancumsum # Cumulative sum 
cummax # Cumulative max 
cummin  # Cumulative min 
cumprod # Cumulative prod 
pmax  # Element-wise max 
pmin  # Element-wise min
```

(<a href="#top">Back to top</a>)
<hr>

### recoding missing values
```R
leadership$age[leadership$age == 99] <- NA
```

(<a href="#top">Back to top</a>)
<hr>

### dropping columns
```R
myvars <- names(leadership) %in% c("q3", "q4")
newdata <- leadership[!myvars]
# or just selecting the ones to be used
myvars <- c("q1", "q2", "q3", "q4", "q5")newdata <-leadership[myvars]
```

# Rows

## Info

## Selecting

### Columns
```R
dplyr::filter(iris, Sepal.Length > 7)   # Extract rows that meet logical criteria.
dplyr::sample_frac(iris, 0.5, replace = TRUE)  # Randomly select fraction of rows.
dplyr::sample_n(iris, 10, replace = TRUE) # Randomly select n rows.
dplyr::slice(iris, 10:15) # Select rows by position.
dplyr::top_n(storms, 2, date)   # Select and order top n entries (by group if grouped data).
```

(<a href="#top">Back to top</a>)
<hr>


### slice by data range
```R
startdate <- as.Date("2009-01-01")
enddate   <- as.Date("2009-10-31")
newdata <- leadership[which(leadership$date >= startdate &
leadership$date <= enddate),]
```

```R
dplyr::
select(iris, Sepal.Width, Petal.Length, Species)
select(iris, contains("."))  # name contains a character string.
select(iris, ends_with("Length"))  # name ends with a character string.
select(iris, everything())   # every column.
select(iris, matches(".t."))  # name matches a regular expression.
select(iris, num_range("x", 1:5))  # columns named x1, x2, x3, x4, x5.
select(iris, one_of(c("Species", "Genus")))  # in a group of names.
select(iris, starts_with("Sepal"))   # starts with a character string.
select(iris, Sepal.Length:Petal.Width)  # all columns between Sepal.Length and Petal.Width (inclusive).
select(iris, -Species)  # all columns except Species.
```

(<a href="#top">Back to top</a>)
<hr>


### Conditional selection
```R
df[Gender =="MALE",]  # matching column value
df$Age.At.Death[3]
iris$Sepal.Length[1:10]

if('Id' %in% names(test)){

}

full_imp[which(is.na(age), arr.ind = T), ] # is.na (select all where age-values are na)
```

(<a href="#top">Back to top</a>)
<hr>

### Regex
```R
df[grep("4", writers_df$Age.At.Death),]
```

## Changing

## Manipulating

### Removing
```R
dplyr::distinct(iris) # Remove duplicate rows.
```

(<a href="#top">Back to top</a>)
<hr>



## Changing

### Rename column labels
```R
library("dplyr")idata = rename(idata, Country = `Country Name`)
# or
library(reshape)leadership <- rename(leadership,                     c(manager="managerID", date="testDate"))
```

```R
# The dplyr way (rename two variables)idata = rename(idata,
	top10 = `Income share held by highest 10% [SI.DST.10TH.10]`, 
	bot10 = `Income share held by lowest 10% [SI.DST.FRST.10]`)# The base R way (rename five variables)names(idata)[5:9] = c("top10", "bot10", "gini", "b40_cons", "gdp_percap")
```

(<a href="#top">Back to top</a>)
<hr>


### Classes

```R
idata = readRDS("data/idata-renamed.Rds")sapply(idata, class)#> Country Country Code Year Year Code top10 #> "character" "character" "integer" "character" "character" #> bot10 gini b40_cons gdp_percap#> "character" "character" "character" "character"
```

(<a href="#top">Back to top</a>)
<hr>


# Cells

## Manipulating

### Changing
```R
mydata$size[mydata$individual == 15] <- c(20.3)
```

or

```R
mydata[3,2] <- c(20.3)
```

(<a href="#top">Back to top</a>)
<hr>


# Joining / Merging

![{{base}}/images/lambda_architecture.png]({{base}}/images/datascience/R_rbind_cbind.png)
[image source](http://cfile7.uf.tistory.com/image/2745533555B5F2C203AC87)


```R
rbind
sample1 <- data[sample(1:nrow(data), 10, replace=FALSE),]
sample2 <- data[sample(1:nrow(data), 5, replace=FALSE),]
newdata <- rbind(sample1, sample2)
```

```R
# cbind
newdata1 <- data[c(1,5:7)]
newdata2 <- data[c(8:11)]
newdata <- cbind(newdata1, newdata2)
```

(<a href="#top">Back to top</a>)
<hr>


## Merging

```R
total <- merge(dataframeA, dataframeB, by="ID")
```

(<a href="#top">Back to top</a>)
<hr>


## Variables btw dataframes
```R
birds$elevation <- sites$elevation[match(birds$siteno, sites$siteno)]
```


(<a href="#top">Back to top</a>)
<hr>



# Stats


```R
#number of elements in column
length(test.dates)
```

(<a href="#top">Back to top</a>)
<hr>


## Analyze a single variable

```R
mean(mydata$size.mm, na.rm = TRUE)   # na.rm option removes missing values
```

(<a href="#top">Back to top</a>)
<hr>


## Apply the same function to several variables at once
The two (lapply and sapply) are equivalent but differ in the format of their output

```R
myresult <- sapply(mydata[,2:5], FUN = mean, na.rm = TRUE)
mylist <- lapply(mydata[,2:5], FUN = mean, na.rm = TRUE)
```

(<a href="#top">Back to top</a>)
<hr>


## Math

### Quantile
```R
y <- quantile(roster$score, c(.8,.6,.4,.2))
```


(<a href="#top">Back to top</a>)
<hr>



## frequency table

### of column values

```R
names <- c(df$Name)
name_freq <- table(names)/length(names)
```

(<a href="#top">Back to top</a>)
<hr>


## missingness & new zero variance
```R
summary(sapply(training, is.na)) # any missing values? nope
nearZeroVar(training)
```

(<a href="#top">Back to top</a>)
<hr>


## Variability

## too many levels (e.g. > 20)
```R
factors <- which(sapply(ds[vars], is.factor))
lvls    <- sapply(factors, function(x) length(levels(ds[[x]])))
(many   <- names(which(lvls > 20)))
```

(<a href="#top">Back to top</a>)
<hr>

## character(0)
```R
ignore  <- union(ignore, many)
```

(<a href="#top">Back to top</a>)
<hr>

## constants | unique values
```R
(constants <- names(which(sapply(ds[vars], function(x) all(x == x[1L])))))
```

(<a href="#top">Back to top</a>)
<hr>

## location
```R
(ids   <- which(sapply(ds, function(x) length(unique(x))) == nrow(ds)))

ignore <- union(ignore, constants)
```

(<a href="#top">Back to top</a>)
<hr>

## Covariance and correlation
```R
cov(iris[,1:4]) # covariance
cor(iris[,1:4]) # correlation
```

```R
mc <- cor(ds[which(sapply(ds, is.numeric))], use="complete.obs")
mc[upper.tri(mc, diag=TRUE)] <- NA
# pipe df through different functions
mc <-
  mc %>%
  abs() %>%
  data.frame() %>%
  mutate(var1=row.names(mc)) %>%
  gather(var2, cor, -var1) %>%
  na.omit()
mc <- mc[order(-abs(mc$cor)),]
mc
# and then add to ignore list
ignore <- union(ignore, c("temp_3pm", "pressure_9am", "temp_9am"))
```

(<a href="#top">Back to top</a>)
<hr>

## matrix of scatter plots
```R
pairs(iris)
```

(<a href="#top">Back to top</a>)
<hr>

# Sorting

## rows (according to column age.as.writer)

```R
writers_df[order(writers_df$Age.As.Writer),]
writers_df[order(writers_df$Age.As.Writer, decreasing=TRUE),]
writers_df[order(-writers_df$Age.As.Writer),] # numeric variable
```

(<a href="#top">Back to top</a>)
<hr>

## with dplyr

```R
data2 <- arrange(writers_df, Age.At.Death, Age.As.Writer)
    # or 
writers_df[with(writers_df, order(Age.At.Death, Age.As.Writer)), ]
    # desc order
desc_sorted_data <- arrange(writers_df, desc(Age.At.Death))
```

(<a href="#top">Back to top</a>)
<hr>

## Benchmarking

```R
library("microbenchmark")df = data.frame(v = 1:4, name = c(letters[1:4])) 
microbenchmark(  df[3, 2],  df$name[3],  df[3, 'v'])#> Unit: microseconds#>        expr  min   lq mean median   uq   max neval#>    df[3, 2] 22.8 24.2 27.6   24.8 25.5 201.3   100#>  df$name[3] 16.2 17.6 19.9   18.9 19.7  62.4   100#>  df[3, "v"] 14.8 15.9 17.0   16.5 17.0  30.0   100
```

(<a href="#top">Back to top</a>)
<hr>

## Profiling
```R
library("profvis") profvis(expr = {  # Stage 1: load packageslibrary("rnoaa") library("ggplot2")  # Stage 2: load and process dataout = readRDS("data/out-ice.Rds")df = dplyr::rbind_all(out, id = "Year")  # Stage 3: visualise output
  
ggplot(df, aes(long, lat, group = paste(group, Year))) + geom_path(aes(colour = Year))ggsave("figures/icesheet-test.png")}, interval = 0.01, prof_output = "ice-prof")
```

(<a href="#top">Back to top</a>)
<hr>

## Caching

```R
# Argument indicates row to removeplot_mpg = function(row_to_remove) { 
	data(mpg, package="ggplot2")	mpg = mpg[-row_to_remove,] 
	plot(mpg$cty, mpg$hwy) 
	lines(lowess(mpg$cty, mpg$hwy), col=2)
}
```
and then a quick benchmark

```R
library("memoise")m_plot_mpg = memoise(plot_mpg)microbenchmark(times=10, unit="ms", m_plot_mpg(10), plot_mpg(10)) 
#> Unit: milliseconds#> expr min lq mean median uq max neval cld 
#> m_plot_mpg(10) 0.04 4e-02 0.07 8e-02 8e-02 0.1 10 a 
#> plot_mpg(10) 40.20 1e+02 95.52 1e+02 1e+02 107.1 10 b
```

(<a href="#top">Back to top</a>)
<hr>

# Control structure

## If-else
```R
if(<condition>) {	## do something} else {}
```

```R
if (is.character(grade)) grade <- as.factor(grade)
if (!is.factor(grade)) grade <- as.factor(grade) else print("Grade already
    is a factor")
 ```

```R
ifelse(score > 0.5, print("Passed"), print("Failed"))
outcome <- ifelse (score > 0.5, "Passed", "Failed")
# M || F
psub$SEX = as.factor(ifelse(psub$SEX==1,'M','F'))
```

```R
if(<condition1>) {## do something} else if(<condition2>) {## do something different} else {## do something different}
```

(<a href="#top">Back to top</a>)
<hr>

## Loop

### through subset of data
```R
for(i in c(2,6,10:15)){
  print( sd(mydata[,i], na.rm=TRUE) )
  }
```


(<a href="#top">Back to top</a>)
<hr>

