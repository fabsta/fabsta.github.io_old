---
title: "Python Data Cleaning Engineering Sheet"
description: "Python Data Cleaning Engineering Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---

# Table of contents

* TOC
{:toc}


# Getting Started with pandas

(<a href="#top">Back to top</a>)
<hr>

## Essential Functionality

(<a href="#top">Back to top</a>)
<hr>
## Summarizing and Computing Descriptive Statistics

### Sum, Describe

### Correlation / Covariance
```python
df.corr()
```

### Unique Values, Value Counts, and Membership

#### Compute value frequencies
```python
obj.value_counts()
```

```python
c    3
a    3
b    2
d    1
```



(<a href="#top">Back to top</a>)
<hr>
## Correlation Matrix Of Values

```python
df = df.corr()
df.rolling_mean(df, 2)  # Calculate the moving average. That is, take
                        # the first two values, average them, 
                        # then drop the first and add the third, etc.
```

(<a href="#top">Back to top</a>)
<hr>

## Handling Missing Data

### using mean
```python
df['column'].fillna(df['column'].mean(), inplace=True)
# mean by other column category
df['column'].fillna(df.groupby('column2')['column'].transform("mean"), inplace=True) 
```

```python
def compute_mean(data_frame, column):
    columnName = str(column)
    meanValue = data_frame[columnName].dropna().mean()
    if len(data_frame.column[data_frame.column.isnull()]) > 0:
        data_frame.loc[(data_frame.column.isnull()), columnName] = meanValue
```
(<a href="#top">Back to top</a>)
<hr>

### replacing data
```python
df.fillna({1: 0.5, 3: -1})
data.replace([-999, -1000], [np.nan, 0]) # 999 -> np.nan, -1000 -> 0
df.fillna(0, inplace=True) # np.nan -> 0s = df['col'].fillna(0)          # np.nan -> 0df = df.replace(r'\s+', np.nan,regex=True) # white space -> np.nan```

(<a href="#top">Back to top</a>)
<hr>


## Hierarchical Indexing


# Data Wrangling: Clean, Transform, Merge, Reshape

## Combining and Merging Data Sets

## Reshaping and Pivoting

## Data Transformation


### Numbers

#### Rounding off location coordinates to 2 decimal points

```python
data_frame.X = data_frame.X.map(lambda x: "%.2f" % round(x, 2)).astype(float)
or
format = lambda x: '%.2f' % x
frame.applymap(format)
```

(<a href="#top">Back to top</a>)
<hr>    

#### Detecting and Filtering Outliers
```python
data.describe()
```
```python
                 0            1            2            3
count  1000.000000  1000.000000  1000.000000  1000.000000
mean     -0.067684     0.067924     0.025598    -0.002298
std       0.998035     0.992106     1.006835     0.996794
min      -3.428254    -3.548824    -3.184377    -3.745356
25%      -0.774890    -0.591841    -0.641675    -0.644144
50%      -0.116401     0.101143     0.002073    -0.013611
75%       0.616366     0.780282     0.680391     0.654328
max       3.366626     2.653656     3.260383     3.927528
```

Select all rows exceeding -3 or 3

```python
data[(np.abs(data) > 3).any(1)]
```

Set all rows exceeding -3 or 3

```python
data[np.abs(data) > 3] = np.sign(data) * 3
```

The ufunc np.sign returns an array of 1 and -1 depending on the sign of the values.

(<a href="#top">Back to top</a>)
<hr>

### String    

#### String to Integer
```python
# 1. determine all values
Categories = list(enumerate(sorted(np.unique(data_frame['Category']))))
# 2. set up dictionaries
CategoriesDict = {name: i for i, name in Categories}
# 3. Convert all strings to int
data_frame.Category = data_frame.Category.map(lambda x: CategoriesDict[x]).astype(int)
```

(<a href="#top">Back to top</a>)
<hr>    


#### String Manipulation: "/" -> 0|1
```python
data['StreetCorner'] = df['Address'].str.contains('/').map(int)
```

(<a href="#top">Back to top</a>)
<hr>    


#### DayOfWeek

```python
DayOfWeeks = df.DayOfWeek.unique()
    DayOfWeekMap = {}
    i = 0
    for s in DayOfWeeks:
        DayOfWeekMap[s] = i
        i += 1
    data = data.join(df['DayOfWeek'].map(DayOfWeekMap))
```

(<a href="#top">Back to top</a>)
<hr>

#### Convert Dates
```python
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

(<a href="#top">Back to top</a>)
<hr>

####  Computing Indicator/Dummy Variables

```python
dummies = pd.get_dummies(df['key'], prefix='key')
df_with_dummy = df[['data1']].join(dummies)
```

```python
   data1  key_a  key_b  key_c
0      0      0      1      0
1      1      0      1      0
2      2      1      0      0
3      3      0      0      1
4      4      1      0      0
5      5      0      1      0
```


(<a href="#top">Back to top</a>)
<hr>


# Data Aggregation and Group Operations

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/group_aggregation.png)
[image source](https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/httpatomoreillycomsourceoreillyimages1346942.png)

## Group by  + mean
```python
means = df['data1'].groupby([df['key1'], df['key2']]).mean()
```

```python
key1  key2
a     one     0.880536
      two     0.478943
b     one    -0.519439
      two    -0.555730
```

(<a href="#top">Back to top</a>)
<hr>

## Iterating over groups

```python
for name, group in df.groupby('key1'):
	print name
	print group
```


## Pivot Tables


# Unsorted

## Count the number of times each number of deaths occurs in each regiment

```python
 Input
	guardCorps	corps1	corps2	corps3	corps4``````	corps5	corps6	corps7	corps8	corps9	corps10	corps11	corps14	corps15
 1875	0	0	0	0	0	0	0	1	1	0	0	0	1	0
 1876	2	0	0	0	1	0	0	0	0	0	0	0	1	1
 1877	2	0	0	0	0	0	1	1	0	0	1	0	2	0
```
 
```python
result = horsekick.apply(pd.value_counts).fillna(0); result
```

(<a href="#top">Back to top</a>)
<hr>

## Create a crosstab table by company and regiment


```python
 regiment	company	experience	name	preTestScore	postTestScore
 0	Nighthawks	infantry	veteran	Miller	4	25
 1	Nighthawks	infantry	rookie	Jacobson	24	94
 2	Nighthawks	cavalry	veteran	Ali	31	57
 -->
 company	cavalry	infantry	All
 regiment			
 Dragoons	2	2	4
 Nighthawks	2	2	4
```

(<a href="#top">Back to top</a>)
<hr>

## Counting the number of observations by regiment and category

```python
pd.crosstab(df.regiment, df.company, margins=True)
```

(<a href="#top">Back to top</a>)
<hr>

## ?

```python
df['preTestScore'].idxmax() # row with max value
```

(<a href="#top">Back to top</a>)
<hr>


