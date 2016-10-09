---
title: "Data Cleaning Engineering Sheet"
description: "Data Cleaning Engineering Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---

<table>
<tr>
<th>
```R just a test
```</th>
</tr>
<tr>
<td></td>
</tr>
</table>



# Table of contents

* TOC
{:toc}


# Getting Started with R

(<a href="#top">Back to top</a>)
<hr>

## Essential Functionality

### Preparation

```R
# using tbl_df for better printing
library(dplyr)
df <- tbl_df(df)class(df)
# use rattle to normalize variable names
names(df) <- normVarNames(names(df))
```

(<a href="#top">Back to top</a>)
<hr>

## Exploration

### Get examples for each column

```R
str(df)
t(df)[,1:2]
```

(<a href="#top">Back to top</a>)
<hr>

### Distribution of column

```python
# Python
df.describe()
df['glob_IsWon'].value_counts()
```

```R
# R
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

(<a href="#top">Back to top</a>)
<hr>

### Types/classes

```R
# R

table(sapply(df, class))
or
data_types <- sapply(names(df),function(x){class(df[[x]])})
table(data_types)
```

(<a href="#top">Back to top</a>)
<hr>

### Select only (numeric | logical ) features
```R
# R

nums <- sapply(x, is.numeric | is.logical)
# Then standard subsetting
x[ , nums] || x[,!nums] for the opposite
```

### Charts

#### Pie 

```R
# R

pie(table(df$glob_IsWon))
```

#### Histogram

```python
# Python
df['ApplicantIncome'].hist(bins=50)
```

```R
# R
hist(df$StageIdList)
```

#### Scatterplot

```R
plot(iris$Sepal.Length, iris$Sepal.Width)
```

#### Boxplot

```python
# Python
df.boxplot(column='ApplicantIncome')
df.boxplot(column='ApplicantIncome', by = 'Education')
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

(<a href="#top">Back to top</a>)
<hr>

### Variable roles
```R
# R
target <- "rain_tomorrow"risk   <- "risk_mm"id     <- c("date", "location")

predictorNames <- setdiff(names(traindf), outcomeName)
```

(<a href="#top">Back to top</a>)
<hr>

## Summarizing and Computing Descriptive Statistics

(<a href="#top">Back to top</a>)
<hr>

### Unique values 

```R
unique(df['glob_IsWon'])
```

(<a href="#top">Back to top</a>)
<hr>

### Missing values
```python
# Python
df.apply(lambda x: sum(x.isnull()),axis=0) 
```

### Sum, Describe

#### Sum + plot using pipeline
```R
data %>%
  select(SVM, `Random Forest`, `Neural Net`, GBM) %>%
  gather(method, used) %>%
  group_by(method) %>%
  summarise(percent_used = sum(used) / n()) %>%
  ggplot(aes(method, percent_used)) +
  geom_bar(stat = 'identity') +
  labs(x = "Method", y = "% of posts")
```

(<a href="#top">Back to top</a>)
<hr>

### Correlation / Covariance

```python
# Python
df.corr()
```

```R
# R
df.cor
### highly correlated variables
mc <- cor(ds[which(sapply(ds, is.numeric))], use="complete.obs")mc[upper.tri(mc, diag=TRUE)] <- NAmc <-  mc %>%  abs() %>%  data.frame() %>%  mutate(var1=row.names(mc)) %>%  gather(var2, cor, -var1) %>%  na.omit()mc <- mc[order(-abs(mc$cor)),]mc
```



### Variance

#### zero Variance

```R
df_new <- df[sapply(df, function(x) length(levels(factor(x)))>1)]
# or
(ids   <- which(sapply(ds, function(x) length(unique(x))) == nrow(ds)))
```

(<a href="#top">Back to top</a>)
<hr>

#### near zero variance
```R
nzv_cols <- nearZeroVar(GermanCredit)
# If you want to save metrics
nzv_cols <- nearZeroVar(GermanCredit, saveMetrics = TRUE)
if(length(nzv_cols) > 0) GermanCredit <- GermanCredit[, -nzv_cols]
```

(<a href="#top">Back to top</a>)
<hr>

### Unique Values, Value Counts, and Membership

#### Compute value frequencies
```R
```


(<a href="#top">Back to top</a>)
<hr>



# Data Wrangling: Clean, Transform, Merge, Reshape
[tidy-data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)

## Feature understanding

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

(<a href="#top">Back to top</a>)
<hr>

## Standardizing

#### Scaling

Standardizes the specified columns of a matrix or data frame to a mean of 0 and a standard deviation of 1

```R
newdata <- scale(mydata)
z <- scale(df[,2:4])
```


```R
newdata <- scale(mydata)*SD + M
newdata <- transform(mydata, myvar = scale(myvar)*10+50)
```

[why scaling + normalization is good](https://www.quora.com/When-should-you-perform-feature-scaling-and-mean-normalization-on-the-given-data-What-are-the-advantages-of-these-techniques)
 

(<a href="#top">Back to top</a>)
<hr>


## Combining and Merging Data Sets

Joins

(<a href="#top">Back to top</a>)
<hr>

## Reshaping and Pivoting

![{{base}}/images/lambda_architecture.png]({{base}}/images/datascience/R_gather_spread.png)

[image source](http://www.sthda.com/sthda/RDoc/images/tidyr.png)

(<a href="#top">Back to top</a>)
<hr>

#### vector -> column

```R
cbind(sort(test_adj))
```

(<a href="#top">Back to top</a>)
<hr>

### collapse columns

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


## Data Transformation

### 1 column -> 1 column

#### mutate  - revalue

```R
data = data %>%
  mutate(CalculatedProgressStage_new = revalue(CalculatedProgressStage,
                                   c("APPROACH" = "aufgehts",
                                     "NEGOTIATE" = "verhandelne",
                                     "QUALIFY" = "other handpump"
                                     )))
```

(<a href="#top">Back to top</a>)
<hr>

#### if-else

```R
outcome <- ifelse (score > 0.5, "Passed", "Failed")
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

titanic-example

```R
ifelse(grepl('Mr ', titanicDF$Name), 'Mr', ifelse(grepl('Mrs ', titanicDF$Name), 'Miss', 'Nothing'))
```

(<a href="#top">Back to top</a>)
<hr>    

#### Recoding Variables


##### Continuous into categories
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

(<a href="#top">Back to top</a>)
<hr>    

### 1 column -> x columns

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



### x columns -> 1 column

```R
```

(<a href="#top">Back to top</a>)
<hr>

### x columns -> y columns

```R
billboard3 <- billboard2 %>%
  mutate(
    week = extract_numeric(week),
    date = as.Date(date.entered) + 7 * (week - 1)) %>%
  select(-date.entered)
```

for many columns

```R
#convert numbers to numeric data
spine[,1:12]=data.matrix(spine[,1:12])
```

(<a href="#top">Back to top</a>)
<hr>


### Formats

#### Check correct
```R
is.numeric(df$target)
is.factor(df$target)
is.character(df$target)
```

#### Character types

```R
mydata$x <- as.factor(mydata$x)     # character to factor 
mydata$x <- as.character(mydata$x)  # factor to character
extract_numeric(week)
as.Date(date.entered)
```



# Data Wrangling: Clean, Transform, Merge, Reshape

## Combining and Merging Data Sets

## Reshaping and Pivoting

## Data Transformation

#### Factor

```R
# R
df$target <- factor(df$target2, labels = c("won", "lost"))
```
explained [here](http://www.ats.ucla.edu/stat/r/modules/factor_variables.htm)

### Strings

```python
# Python
# 1. determine all values
Categories = list(enumerate(sorted(np.unique(data_frame['Category']))))
# 2. set up dictionaries
CategoriesDict = {name: i for i, name in Categories}
# 3. Convert all strings to int
data_frame.Category = data_frame.Category.map(lambda x: CategoriesDict[x]).astype(int)
```

### Numbers

#### Rounding off location coordinates to 2 decimal points

```python
data_frame.X = data_frame.X.map(lambda x: "%.2f" % round(x, 2)).astype(float)
or
format = lambda x: '%.2f' % x
frame.applymap(format)
```

```R
# R
# Convert all logical columns to numeric
cols <- sapply(dat, is.logical)
dat[,cols] <- lapply(dat[,cols], as.numeric)
#
as.factor
as.numeric
as.logical
as.character
```

(<a href="#top">Back to top</a>)
<hr>

#### Dates 

```python
# Python
date_time = pd.to_datetime(df.Dates)
year = date_time.dt.year
data['Year'] = year
month = date_time.dt.month
data['Month'] = month
day = date_time.dt.day
data['Day'] = day
hour = date_time.dt.hour
data['hour'] = hour
minute = date_time.dt.minute
time = hour*60+minute
data['Time'] = time
```

```R
# R
mydates <- as.Date(c("2007-06-22", "2004-02-13"))
#
strDates <- c("01/05/1965", "08/16/1975")
dates <- as.Date(strDates, "%m/%d/%Y")
```
R stores dates internally, they’re represented as the number of days since January 1, 1970,

##### as weekday
```python
# Python
DayOfWeeks = df.DayOfWeek.unique()
    DayOfWeekMap = {}
    i = 0
    for s in DayOfWeeks:
        DayOfWeekMap[s] = i
        i += 1
    data = data.join(df['DayOfWeek'].map(DayOfWeekMap))
```

```R
# R
weekdays(as.Date('16-08-2012','%d-%m-%Y'))
```

##### day in week to 'workweek' 'weekend'

```R
# R
data$day = factor(NA,levels=c('workweek','weekend'))
data$day[day >= 0 & day < 5] <- 'workweek'
data$day[day >= 5] <- 'weekend'
```

##### date difference

```R
# R
today <- Sys.Date()
dob   <- as.Date("1956-10-12")
difftime(today, dob, units="weeks")
>Time difference of 2825 weeks
```


(<a href="#top">Back to top</a>)
<hr>






## Handling Missing Data

### Replacing NAs 

```python
# Python
df.fillna({1: 0.5, 3: -1})
data.replace([-999, -1000], [np.nan, 0]) # 999 -> np.nan, -1000 -> 0
df.fillna(0, inplace=True) # np.nan -> 0s = df['col'].fillna(0)          # np.nan -> 0df = df.replace(r'\s+', np.nan,regex=True) # white space -> np.nan
```

#### replace all NAs with mean

```python
# Python
df['column'].fillna(df['column'].mean(), inplace=True)
# mean by other column category
df['column'].fillna(df.groupby('column2')['column'].transform("mean"), inplace=True) 

# mean-function
def compute_mean(data_frame, column):
    columnName = str(column)
    meanValue = data_frame[columnName].dropna().mean()
    if len(data_frame.column[data_frame.column.isnull()]) > 0:
        data_frame.loc[(data_frame.column.isnull()), columnName] = meanValue
```

```R
# R
for(i in 1:ncol(df)){
    cat("checking col: ",str(i),df[names())
    df[is.na(df[,i]), i] <- mean(df[,i], na.rm = TRUE)
}
# treat integer and character differently
for (x in attr.data.types$integer){
  sample.df[[x]][is.na(sample.df[[x]])] <- -1
}
#
for (x in attr.data.types$character){
  sample.df[[x]][is.na(sample.df[[x]])] <- "*MISSING*"
}
```

(<a href="#top">Back to top</a>)
<hr>    

#### using linear regression
 create shadow matrix

```R
x <- as.data.frame(abs(is.na(sleep)))
y <- x[which(sd(x) > 0)]# extracts the variables that have some (but not all) missing values, andcor(y)
```
gives you correlations among indicator variables. of missing values.

(<a href="#top">Back to top</a>)
<hr>    

##### applying linear regression

```R
# R
## impute missing values with linear regression
imput_age <- lm(age~., data = full_imp)
summary(imput_age)
imp_age <- predict(imput_age, full_imp[which(is.na(age), arr.ind = T), ])
#select all where age is NA
full_imp[is.na(full_imp[, age]), age := .(imp_age)]
```

(<a href="#top">Back to top</a>)
<hr>

### recoding missing values

```R
leadership$age[leadership$age == 99] <- NA
```

(<a href="#top">Back to top</a>)
<hr>

#### removing rows with 'na' values using na.omit

```R
newdata <- na.omit(df)
```
![{{base}}/images/lambda_architecture.png]({{base}}/images/datascience/R_na_omit.jpg)

[image source](https://www.safaribooksonline.com/library/view/r-in-action/9781935182399/04list04_alt.jpg)




(<a href="#top">Back to top</a>)
<hr>

#### Binning Data

```python
# Python
date_time = pd.to_datetime(df.Dates)
year = date_time.dt.year
data['Year'] = year
month = date_time.dt.month
data['Month'] = month
day = date_time.dt.day
data['Day'] = day
hour = date_time.dt.hour
data['hour'] = hour
minute = date_time.dt.minute
time = hour*60+minute
data['Time'] = time
```

(<a href="#top">Back to top</a>)
<hr>

#### Binning Data
```python
bins = [0, 25, 50, 75, 100]   ## define bin ranges
group_names = ['Low', 'Okay', 'Good', 'Great']

categories = pd.cut(df['postTestScore'], bins, labels=group_names)
df['categories'] = pd.cut(df['postTestScore'], bins, labels=group_names)

ages = [20, 22, 25, 27, 21, 23, 37, 31, 61, 45, 41, 32]
bins = [18, 25, 35, 60, 100]
cats = pd.cut(ages, bins) 
```

```R
# R
dat <- read.table("clipboard", header=TRUE)

cuts <- apply(dat, 2, cut, c(-Inf,seq(0.5, 1, 0.1), Inf), labels=0:6)
cuts[cuts=="6"] <- "0"
cuts <- as.data.frame(cuts)
  cosinFcolor cosinEdge cosinTexture histoFcolor histoEdge histoTexture jaccard
1           3         0            0           1         1            0       0
2           0         0            5           0         2            2       0
3           1         0            2           0         0            1       0
4           0         0            3           0         1            1       0
5           1         3            1           0         4            0       0
6           0         0            1           0         0            0       0
```

[stackoverflow](http://stackoverflow.com/questions/11963508/generate-bins-from-a-data-frame)


```R
x<-rnorm(1000, mean=0, sd=50)
summary(x)
Min. 1st Qu. Median Mean 3rd Qu. Max.
-157.1000 -32.9200 -0.5643 0.7896 34.0000 148.3000
Next, let's say we want to create ten bins with equal number of observations in each bin

bins<-10
cutpoints<-quantile(x,(0:bins)/bins)
The cutpoints variable holds a vector of the cutpoints used to bin the data. Finally we perform the binning itself to form the discretized variable

binned <-cut(x,cutpoints,include.lowest=TRUE)
summary(binned)
```

(<a href="#top">Back to top</a>)
<hr>

####  Computing Indicator/Dummy Variables

```python
# Python
dummies = pd.get_dummies(df['key'], prefix='key')
df_with_dummy = df[['data1']].join(dummies)
```

```R
# R
dummy <- dummyVars("~.", data=df, fullRank=F)
df <- as.data.frame(predict(dummy, df))
```


(<a href="#top">Back to top</a>)
<hr>


## Filtering / Removing

### Remove columns with standard deviation of zero
```R
all_sd_zero <- sapply(df, function(x) { sd(x) == 0})
# use sd(data$var, na.rm=TRUE) to ignore NA values
df <- df[!all_sd_zero]
```

(<a href="#top">Back to top</a>)
<hr>

### List of useful cleaning operations

```R
# only unique
(ids   <- which(sapply(ds, function(x) length(unique(x))) == nrow(ds)))
ignore <- union(ignore, names(ids))
# all missing
mvc <- sapply(ds[vars], function(x) sum(is.na(x)))mvn <- names(which(mvc == nrow(ds)))ignore <- union(ignore, mvn)
# many missing
mvn <- names(which(mvc >= 0.7*nrow(ds)))ignore <- union(ignore, mvn)
# too many levels
factors <- which(sapply(ds[vars], is.factor))lvls    <- sapply(factors, function(x) length(levels(ds[[x]])))(many   <- names(which(lvls > 20)))
ignore  <- union(ignore, many)
# constants
(constants <- names(which(sapply(ds[vars], function(x) all(x == x[1L])))))
ignore     <- union(ignore, constants)
```

(<a href="#top">Back to top</a>)
<hr>


(<a href="#top">Back to top</a>)
<hr>

# Data Aggregation and Group Operations


## Group by  + mean
```python
# Python
means = df['data1'].groupby([df['key1'], df['key2']]).mean()
```

```R
# R
```

(<a href="#top">Back to top</a>)
<hr>

# Feature selection

## univariate selection
```R
# R
```

[source](http://blog.datadive.net/selecting-good-features-part-i-univariate-selection/)

(<a href="#top">Back to top</a>)
<hr>

## using machine learning

### fscaret - ensemble-based feature selection
```R
splitIndex <- createDataPartition(df$target, p = .75, list = FALSE, times = 1)
trainDF <- df[splitIndex,]
testDF <- df[-splitIndex,]
fsModels <- c("glm","gbm","treebag","ridge","lasso")

myFS<-fscaret(trainDF, testDF, myTimeLimit = 40, preprocessData=TRUE,
              Used.funcRegPred = 'gbm', with.labels=TRUE,
              supress.output=FALSE, no.cores=2)

myFP$PPlabels
```

[source](http://amunategui.github.io/fscaret-Walkthrough/)

(<a href="#top">Back to top</a>)
<hr>

# Training

## Split training/test data
```R
Train <- createDataPartition(GermanCredit$Class, p=0.6, list=FALSE)
training <- GermanCredit[ Train, ]
testing <- GermanCredit[ -Train, ]
```

alternatively

```R
train_ind = sample(1:n, size = round(0.8*n), replace=FALSE)
#
train = spine_red[train_ind,]
test = spine_red[-train_ind,]
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
