---
title: "R Cheat Sheet"
description: "R Cheat Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---


[this cheat sheet is based on the fantastic work by @Mark_Graph]. 

# Table of contents

* TOC
{:toc}


# Preliminaries
```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from pandas import DataFrame, Series
```

(<a href="#top">Back to top</a>)
<hr>

# Input / Output

## Read

### CSV
```R
train <- read.csv("../train.csv", stringsAsFactors = F, row.names = 1)
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

### Custom headers
```R
raw.train <- function(){
  # Loads the training data with correct classes
  cls <- c('factor', 'factor', 'Date', 'numeric', 'logical')
  train <- read.csv(paste0(paths$data, 'train.csv'), 
                    colClasses=cls)
}
```

## Write

### Terminal
```R
cat("simplifying names...\n")
print(paste('dept:', d))
```

### File
```R
write.csv(ss, file = submit.path, quote=FALSE, row.names=FALSE)
```

## Define paths
```R
paths = list(data='../data/',
             submit='../submissions/',
             r='../R/')
.. later
paths$data             
```

# Inspecting
[dplyr tutorial](http://rpubs.com/justmarkham/dplyr-tutorial)

```R
head(train[, -c(1, 5)])
head(mydata, n = 20) # first 20 rows to console
View(mydata)         # spreadsheet view 
str(train)
class(train)         # gets class
dim(writers_df) # check dimensions
names(df)
sapply(ds,class)
attributes(df)    # list of values per variable
```


```R
library(dplyr)
glimpse(data)
```

## Selecting 

### by index,name
```R
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

## Column

```R
I(df, Name =="Jane")
```

### dplyr
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

## Row 

```R
dplyr::filter(iris, Sepal.Length > 7)   # Extract rows that meet logical criteria.
dplyr::distinct(iris) # Remove duplicate rows.
dplyr::sample_frac(iris, 0.5, replace = TRUE)  # Randomly select fraction of rows.
dplyr::sample_n(iris, 10, replace = TRUE) # Randomly select n rows.
dplyr::slice(iris, 10:15) # Select rows by position.
dplyr::top_n(storms, 2, date)   # Select and order top n entries (by group if grouped data).
```


### matching column value
```R
df[Gender =="MALE",]  # matching column value
df$Age.At.Death[3]
iris$Sepal.Length[1:10]
```

### multiple conditions
```R
subset(df, Age.At.Death <= 40 & Age.As.Writer >= 18)
# select columns to show
subset(x = mydat, subset = x1 > 0 & x2 < 0, select = c(x1,x2)) 
```

### regex (colum)
```R
writers_df[grep("4", writers_df$Age.At.Death),]
```



### Conditional
```R
m[m[, "three"] == 11,] # column by name
m[m[,3] == 11,]        # by number
```

### Unique values
```R
df.dates <- unique(df$Date)
```

## Traversal

### exist in columns

```R
if('Id' %in% names(test)){
}
```




## is.na (select all where age-values are na)
```R
full_imp[which(is.na(age), arr.ind = T), ]
```







# Stats

## 
```R
#number of elements in column
length(test.dates)

```


## frequency table

### of column values

```R
names <- c(df$Name)
name_freq <- table(names)/length(names)
```

## missingness & new zero variance
```R
summary(sapply(training, is.na)) # any missing values? nope
nearZeroVar(training)
```



## Variability

## too many levels (e.g. > 20)
```R
factors <- which(sapply(ds[vars], is.factor))
lvls    <- sapply(factors, function(x) length(levels(ds[[x]])))
(many   <- names(which(lvls > 20)))
```

## character(0)
```R
ignore  <- union(ignore, many)
```

## contants | unique values
```R
(constants <- names(which(sapply(ds[vars], function(x) all(x == x[1L])))))
```

## [1] "location"
## or
```R
(ids   <- which(sapply(ds, function(x) length(unique(x))) == nrow(ds)))

ignore <- union(ignore, constants)
```



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

## matrix of scatter plots
```R
pairs(iris)
```



# Sorting

## rows (according to column age.as.writer)

```R
writers_df[order(writers_df$Age.As.Writer),]
writers_df[order(writers_df$Age.As.Writer, decreasing=TRUE),]
writers_df[order(-writers_df$Age.As.Writer),] # numeric variable
```

## with dplyr

```R
data2 <- arrange(writers_df, Age.At.Death, Age.As.Writer)
    # or 
writers_df[with(writers_df, order(Age.At.Death, Age.As.Writer)), ]
    # desc order
desc_sorted_data <- arrange(writers_df, desc(Age.At.Death))
```

