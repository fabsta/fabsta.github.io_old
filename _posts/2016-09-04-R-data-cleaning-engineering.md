---
title: "R Data Cleaning Engineering Sheet"
description: "R Data Cleaning Engineering Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---

# Table of contents

* TOC
{:toc}


# Getting Started with R

(<a href="#top">Back to top</a>)
<hr>

## Essential Functionality

(<a href="#top">Back to top</a>)
<hr>

## Exploration

### Get examples for each column
```R
str(df)
t(df)[,1:2]
```

### Distribution of column
```R
summary(df$glob_IsWon)
# or
table(df$glob_IsWon)
False  True 
  810  1027 
```

things to look for when using summary

* missing values
* invalid values
* outliers 
* data ranges that are too wide or too narrow.


### Charts

#### Pie 

```R
pie(table(df$glob_IsWon))
```

#### Histogram

```R
hist(df$StageIdList)
```

#### Scatterplot

```R
plot(iris$Sepal.Length, iris$Sepal.Width)
```

#### Correlation plot

```R
library(corrplot)
corrplot(cor(X), order = "hclust")
```

#### Bar chart

```R
ggplot(custdata) + geom_bar(aes(x=marital.stat), fill="gray")
```
#### Density plot
```R
library(scales)
#
ggplot(df) + geom_density(aes(x=UserInvolvement_RecencyScore)) +
  scale_x_continuous(labels=dollar)
```

## Summarizing and Computing Descriptive Statistics

### Unique values 

```R
unique(df['glob_IsWon'])
```

### Sum, Describe

### Correlation / Covariance


### Variance

#### zero Variance
```R
df_new <- df[sapply(df, function(x) length(levels(factor(x)))>1)]
```

#### near zero variance
```R
nzv_cols <- nearZeroVar(GermanCredit)
# If you want to save metrics
nzv_cols <- nearZeroVar(GermanCredit, saveMetrics = TRUE)
if(length(nzv_cols) > 0) GermanCredit <- GermanCredit[, -nzv_cols]
```
### Remove columns with standard deviation of zero
```R
all_sd_zero <- sapply(df, function(x) { sd(x) == 0})
# use sd(data$var, na.rm=TRUE) to ignore NA values
df <- df[!all_sd_zero]
```

### Unique Values, Value Counts, and Membership

#### Compute value frequencies
```R
```



(<a href="#top">Back to top</a>)
<hr>

## Correlation Matrix Of Values

```R
```

(<a href="#top">Back to top</a>)
<hr>

## Handling Missing Data

### create shadow matrix

```R
x <- as.data.frame(abs(is.na(sleep)))
y <- x[which(sd(x) > 0)]# extracts the variables that have some (but not all) missing values, andcor(y)
```
gives you correlations among indicator variables. of missing values.


### using linear regression

```R
## impute missing values with linear regression
imput_age <- lm(age~., data = full_imp)
summary(imput_age)
imp_age <- predict(imput_age, full_imp[which(is.na(age), arr.ind = T), ])
#select all where age is NA
full_imp[is.na(full_imp[, age]), age := .(imp_age)]
```

(<a href="#top">Back to top</a>)
<hr>


### replacing data
```R
```

(<a href="#top">Back to top</a>)
<hr>


## Hierarchical Indexing


# Data Wrangling: Clean, Transform, Merge, Reshape
[tidy-data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)

## Business understanding

* Are the features continuous, discrete or none of the above?

* What is the distribution of this feature?

* Does the distribution largely depend on what subset of examples is being considered? 
	* Time-based segmentation? 
	* Type-based segmentation?

* Does this feature contain holes (missing values)?
	* Are those holes possible to be filled, or would they stay forever?
	* If it possible to eliminate them in the future data?

* Are there duplicate and/or intersecting examples?
	* Answering this question right is extremely important, since duplicate or connected data points might significantly affect the results of model validation if not properly excluded.

* Where do the features come from?
	* Should we come up with the new features that prove to be useful, how hard would it be to incorporate those features in the final design?

* Is the data real-time?
	* Are the requests real-time?

* If yes, well-engineered simple features would likely rock.
	* If no, we likely are in the business of advanced models and algorithms.

* Are there features that can be used as the "truth"?

## Combining and Merging Data Sets

## Reshaping and Pivoting

![{{base}}/images/lambda_architecture.png]({{base}}/images/datascience/R_gather_spread.png)
[image source](http://www.sthda.com/sthda/RDoc/images/tidyr.png)


### x columns -> 1 column (using gather)

Gather the non-variable columns into a two-column key-value pair.

Making wide dataset long.

```R
#> # A tibble: 18 x 11
#>                   religion `<$10k` `$10-20k` `$20-30k` `$30-40k` `$40-50k`
#>                      <chr>   <int>     <int>     <int>     <int>     <int>
#> 1                 Agnostic      27        34        60        81        76
#> 2                  Atheist      12        27        37        52        35
#> 3                 Buddhist      27        21        30        34        33
```

Define key-value columns. 

* key: income
* value: frequency
* to gather: all expect religion

```R
pew %>% gather(income, frequency, -religion)
```

with 

```R
#> # A tibble: 180 x 3
#>                   religion income frequency
#>                      <chr>  <chr>     <int>
#> 1                 Agnostic  <$10k        27
```

range of columns, remove 'na' values

```R
gather(week, rank, wk1:wk76, na.rm = TRUE)
```

### Select only numeric features
```R
nums <- sapply(x, is.numeric)
# Then standard subsetting
x[ , nums] || x[,!nums] for the opposite
```

## Data Transformation

### all

```R
billboard3 <- billboard2 %>%
  mutate(
    week = extract_numeric(week),
    date = as.Date(date.entered) + 7 * (week - 1)) %>%
  select(-date.entered)
```

mutate  - revalue

```R
data = data %>%
  mutate(CalculatedProgressStage_new = revalue(CalculatedProgressStage,
                                   c("APPROACH" = "aufgehts",
                                     "NEGOTIATE" = "verhandelne",
                                     "QUALIFY" = "other handpump"
                                     )))
```


replace all NAs with mean

```R
for(i in 1:ncol(df)){
    cat("checking col: ",str(i),df[names())
    df[is.na(df[,i]), i] <- mean(df[,i], na.rm = TRUE)
}
```

(<a href="#top">Back to top</a>)
<hr>

#### 1 column -> x columns

```R
tidy <- tidier %>%
  separate(key, into = c("location", "time"), sep = "\\.") 
```

```R
tidy %>% head(8)
#>   id       trt location time    time
#> 1  1 treatment     work   T1 0.08514
#> 2  2   control     work   T1 0.22544
#> 3  3 treatment     work   T1 0.27453
#> 4  4   control     work   T1 0.27231
#> 5  1 treatment     home   T1 0.61583
#> 6  2   control     home   T1 0.42967
#> 7  3 treatment     home   T1 0.65166
#> 8  4   control     home   T1 0.56774
```

(<a href="#top">Back to top</a>)
<hr>    

#### if-else

```R
outcome <- ifelse (score > 0.5, "Passed", "Failed")
```

(<a href="#top">Back to top</a>)
<hr>    

### Correct format

```R
is.numeric(df$target)
is.factor(df$target)
is.character(df$target)
```

(<a href="#top">Back to top</a>)
<hr>

### Boolean

#### Convert to number
```R
# Convert all to numeric
cols <- sapply(dat, is.logical)
dat[,cols] <- lapply(dat[,cols], as.numeric)
```

(<a href="#top">Back to top</a>)
<hr>

### Numbers


### String    


```R
# nchar(x)
x <- c("ab", "cde", "fghij")
length(x) returns 3
nchar(x[3]) returns 5
# substr
x <- "abcdef"
substr(x, 2, 4) returns “bcd”
# grep
grep("A", c("b","A","c"), fixed=TRUE)
```

(<a href="#top">Back to top</a>)
<hr>

#### String to Integer
```R
```

(<a href="#top">Back to top</a>)
<hr>    


#### String Manipulation: "/" -> 0|1

##### If else on column
```R
frame$twohouses <- ifelse(frame$data>=2, 2, 1)
frame
   data twohouses
1     0         1
2     1         1
3     2         2
4     3         2
5     4         2
...
16    0         1
17    2         2
18    1         1
19    2         2
20    0         1
21    4         2
```

(<a href="#top">Back to top</a>)
<hr>  

##### Grep string -> new column

```R
extractTitle <- function(name){
	name <- as.character(name)
	if(length(grep(“Miss”, name)) > 0){
		return (“Miss”)
	}
	if(length(grep(“Master”, name)) > 0){
		return (“Master”)
	}
	else {
		return (“Miss”)
	}	
}
```

and apply it

```R
titles <- NULL
for (i in 1:nrow(df)){
	titles <- c(titles, extractTitle(df[i,”name”]))
}
df$title <- as.factor(titles)
```

(<a href="#top">Back to top</a>)
<hr>    

### Recoding Variables


#### Continuous into categories
```R
leadership <- within(leadership,{
                     agecat <- NA
                     agecat[age > 75]              <- "Elder"
                     agecat[age >= 55 & age <= 75] <- "Middle Aged"
                     agecat[age < 55]              <- "Young" })
```

```R
df$col[]
```

### recoding missing values

```R
leadership$age[leadership$age == 99] <- NA
```

#### Create pass/fail variable based on set of cutoff scores

#### removing rows with 'na' values using na.omit
```R
newdata <- na.omit(df)
```
![{{base}}/images/lambda_architecture.png]({{base}}/images/datascience/R_na_omit.jpg)
[image source](https://www.safaribooksonline.com/library/view/r-in-action/9781935182399/04list04_alt.jpg)




(<a href="#top">Back to top</a>)
<hr>

### Convert 

#### Character types

```R
mydata$x <- as.factor(mydata$x)     # character to factor 
mydata$x <- as.character(mydata$x)  # factor to character
extract_numeric(week)
as.Date(date.entered)
```

#### to factor
explained [here](http://www.ats.ucla.edu/stat/r/modules/factor_variables.htm)

```R
df$target <- factor(df$target2, labels = c("won", "lost"))
```

#### Dates 

```R
mydates <- as.Date(c("2007-06-22", "2004-02-13"))
#
strDates <- c("01/05/1965", "08/16/1975")
dates <- as.Date(strDates, "%m/%d/%Y")
```
R stores dates internally, they’re represented as the number of days since January 1, 1970,

##### as weekday

```R
weekdays(as.Date('16-08-2012','%d-%m-%Y'))
```

##### day in week to 'workweek' 'weekend'

```R
data$day = factor(NA,levels=c('workweek','weekend'))
data$day[day >= 0 & day < 5] <- 'workweek'
data$day[day >= 5] <- 'weekend'
```

##### date difference
```
today <- Sys.Date()
dob   <- as.Date("1956-10-12")
difftime(today, dob, units="weeks")
>Time difference of 2825 weeks
```


(<a href="#top">Back to top</a>)
<hr>

#### Binning Data
```R
```

(<a href="#top">Back to top</a>)
<hr>

####  Computing Indicator/Dummy Variables

```R
```


(<a href="#top">Back to top</a>)
<hr>


### Standardizing

#### Scale

Standardizes the specified columns of a matrix or data frame to a mean of 0 and a standard deviation of 1

```R
newdata <- scale(mydata)
z <- scale(df[,2:4])
```


```R
newdata <- scale(mydata)*SD + M
newdata <- transform(mydata, myvar = scale(myvar)*10+50)
```

(<a href="#top">Back to top</a>)
<hr>


# Data Aggregation and Group Operations


## Group by  + mean
```R
```

(<a href="#top">Back to top</a>)
<hr>

## Iterating over groups


## Pivot Tables


# Training

## Split training/test data
```R
Train <- createDataPartition(GermanCredit$Class, p=0.6, list=FALSE)
training <- GermanCredit[ Train, ]
testing <- GermanCredit[ -Train, ]
```

(<a href="#top">Back to top</a>)
<hr>

# Use cases

## assign quantiles to student scores
```R
z <- scale(roster[,2:4])
z
        Math Science English
  [1,]  0.013   1.078   0.587
  [2,]  1.143   1.591   0.037
  [3,] -1.026  -0.847  -0.697
  [4,] -1.649  -0.590  -1.247
```

Get a performance score for each student by calculating the row means using the mean() function and adding it to the roster using the cbind() function

```R
score <- apply(z, 1, mean)
roster <- cbind(roster, score)
roster
             Student  Math  Science English   score
1         John Davis  502      95      25     0.559
2    Angela Williams  600      99      22     0.924
3   Bullwinkle Moose  412      80      18    -0.857
4        David Jones  358      82      15    -1.162
```

```R
y <- quantile(roster$score, c(.8,.6,.4,.2))
y
  80%   60%   40%   20%
 0.74  0.44 -0.36 -0.89
```

Recode percentile ranks

```R
roster$grade[score >= y[1]] <- "A"
roster$grade[score < y[1] & score >= y[2]] <- "B"
roster$grade[score < y[2] & score >= y[3]] <- "C"
roster$grade[score < y[3] & score >= y[4]] <- "D"
roster$grade[score < y[4]] <- "F"
roster
             Student Math Science English  score  grade
1         John Davis  502      95      25  0.559      B
2    Angela Williams  600      99      22  0.924      A
3   Bullwinkle Moose  412      80      18 -0.857      D
```

(<a href="#top">Back to top</a>)
<hr>
