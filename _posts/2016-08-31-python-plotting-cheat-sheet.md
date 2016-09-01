---
title: "Python Plotting Cheat Sheet"
description: "Python plotting Cheat Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---
[source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

# Table of contents

* TOC
{:toc}


# Preliminaries
```python
import matplotlib.pyplot as plt
import pandas as pd
```

(<a href="#top">Back to top</a>)
<hr>

# Histogram
```python
fig  = plt.figure()
ax = fig.add_subplot(1,1,1)
ax.hist(df['Column'], bins = 7)
#here you can play with numbers of bins
plt.title("Title")
plt.xlabel("xlabel")
plt.ylabel("ylabel")
plt.show()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Histogram1.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>

# Boxplot
```python
fig  = plt.figure()
ax = fig.add_subplot(1,1,1)
x.boxplot(df['Column'])
plt.show()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Box_Plot_Violin_Plot1.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>

# Violin plot

```python
import seaborn as sns
sns.violinplot(df['Column1'],df['Column2'])
# Variable plot
sns.despine()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Box_Plot_Violin_Plot-300x212.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>

# Bar chart
```python
var  = df.groupby('Column1').Sales.sum()
#grouped sum of sales at gender level
fig = plt.figure()
ax1 = fig.add_subplot(1,1,1)
ax1.set_xlabel('xlabel')
ax1.set_ylabel('ylabel')
ax1.set_title('title')
var.plot(kind='bar')
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/box-plot.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>


# Line chart
```python
var  = df.groupby('Column1').Sales.sum()
#grouped sum of sales at gender level
fig = plt.figure()
ax1 = fig.add_subplot(1,1,1)
ax1.set_xlabel('xlabel')
ax1.set_ylabel('ylabel')
ax1.set_title('title')
var.plot(kind='line')
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Line.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>


# Stacked column chart
```python
var = df.groupby(['sales','predict_sales']).competition.sum()
var.unstack().plot(kind='bar', stacked = True, color = ['red','blue'], grid=False)
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Stacked_Column_Chart.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>


# Scatter plot
```python
fig = plt.figure()
ax1 = fig.add_subplot(1,1,1)
ax.scatter(df['Column1'], df['Column2'])
plt.show()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Scatter_Chart.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>


# Bubble plot
```python
fig = plt.figure()
ax1 = fig.add_subplot(1,1,1)
ax.scatter(df['Column1'], df['Column2'], s=df['Column3'])
plt.show()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Scatter_Bubble_Chart.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>


# Pie chart
```python
var = df.groupby(['competition']).sum().stack()
temp = var.unstack()
type(temp)
x_list = temp['sales']
label_list = temp.index
pyplot.axis('equal')
# the pie chart is oval by default. To make it a circle use pyplot.axis('equal')
plt.pie(x_list, labels = label_list, autopct = "%1.1f%%")
plt.title("title")
plt.show()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Pie.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>


# Heat map

```python
import numpy as np
#Generate a random number, you can refer your data values also
data = np.random.rand(4,2)
rows = list('1234') #rows categories
columns = list('MF') #column categories
fig,ax=plt.subplots()
#Advance color controls
ax.pcolor(data,cmap=plt.cm.Reds,edgecolors='k')
ax.set_xticks(np.arange(0,2)+0.5)
ax.set_yticks(np.arange(0,4)+0.5)
# Here we position the tick labels for x and y axis
ax.xaxis.tick_bottom()
ax.yaxis.tick_left()
#Values against each labels
ax.set_xticklabels(columns,minor=False,fontsize=20)
ax.set_yticklabels(rows,minor=False,fontsize=20)
plt.show()
```

![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Heat.png)<br>
[image source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

(<a href="#top">Back to top</a>)
<hr>

