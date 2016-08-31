---
title: "Python Machine Learning Cheat Sheet"
description: "Python Machine Learning Cheat Sheet"
category: Programming
tags: [programming]
---
[source](https://www.analyticsvidhya.com/blog/2015/05/data-visualization-python/)

# Table of contents

* TOC
{:toc}


# Preparation
## split training data
```python
from sklearn.cross_validation import train_test_split
x_train,x_test, y_train, y_test = train_test_split(X, y, random_state = 1 )
```

(<a href="#top">Back to top</a>)
<hr>


## Linear regression

```python
from sklearn import datasetsboston = datasets.load_boston()
-
from sklearn.linear_model import LinearRegressionlr = LinearRegression()   # instantiate 
-
lr.fit(boston.data, boston.target)LinearRegression(copy_X=True, fit_intercept=True, normalize=False)
-
predictions = lr.predict(boston.data)
-
lr.coef_
zip(boston.feature_names, lr.coef_)
```

## Linear Regression (ridge)

## Logistic Regression

## Gradient Boosting


# Clustering

## KMeans

### Prepare Data
```python
from sklearn.datasets import make_blobsblobs, classes = make_blobs(500, centers=3)
```

### Plot initial clusters
```python
import matplotlib.pyplot as plt
f, ax = plt.subplots(figsize=(7.5, 7.5))ax.scatter(blobs[:, 0], blobs[:, 1], color=rgb[classes])rgb = np.array(['r', 'g', 'b'])ax.set_title("Blobs")
```

### Run KMeans
```python
from sklearn.cluster import KMeanskmean = KMeans(n_clusters=3)kmean.fit(blobs)
kmean.cluster_centers_ # print centers
```

## KKmeans (minibatch for large data)


## Probabilistic clustering with Gaussian Mixture Models


# Classification

## Decision tree

```python
from sklearn import datasetsX, y = datasets.make_classification(n_samples=1000, n_features=3,                                        n_redundant=0)

from sklearn.tree import DecisionTreeClassifier
dt = DecisionTreeClassifier()dt.fit(X, y)

preds = dt.predict(X)(y == preds).mean()
```

## Random Forest

```python
from sklearn import datasets

X, y = datasets.make_classification(1000)    #create the dataset with 1,000 samples

from sklearn.ensemble import RandomForestClassifierrf = RandomForestClassifier()rf.fit(X, y)

print "Accuracy:\t", (y == rf.predict(X)).mean()
print "Total Correct:\t", (y == rf.predict(X)).sum()
```

### Feature importance

```python
rf = RandomForestClassifier(compute_importances=True)rf.fit(X, y)f, ax = plt.subplots(figsize=(7, 5))ax.bar(range(len(rf.feature_importances_)),           rf.feature_importances_)ax.set_title("Feature Importances")
```

### Tuning Random Forest

#### Confusing matrix

```python
import numpy as nptraining = np.random.choice([True, False], p=[.8, .2],                                size=y.shape)from sklearn.ensemble import RandomForestClassifierrf = RandomForestClassifier()rf.fit(X[training], y[training])preds = rf.predict(X[~training])print "Accuracy:\t", (preds == y[~training]).mean()

from sklearn.metrics import confusion_matrixmax_feature_params = ['auto', 'sqrt', 'log2', .01, .5, .99]confusion_matrixes = {}for max_feature in max_feature_params:       rf = RandomForestClassifier(max_features=max_feature)
       rf.fit(X[training], y[training])
```

Look at confusion matrix
```python
import pandas as pdconfusion_df = pd.DataFrame(confusion_matrixes)import itertoolsfrom matplotlib import pyplot as pltf, ax = plt.subplots(figsize=(7, 5))confusion_df.plot(kind='bar', ax=ax)ax.legend(loc='best')ax.set_title("Guessed vs Correct (i, j) where i is the guess and j is                 the actual.")ax.grid()ax.set_xticklabels([str((i, j)) for i, j in                       list(itertools.product(range(2), range(2)))]);ax.set_xlabel("Guessed vs Correct")ax.set_ylabel("Correct")
```

#### Number of Estimators: Iterating through 1 - 20

```python
n_estimator_params = range(1, 20)confusion_matrixes = {}for n_estimator in n_estimator_params:       rf = RandomForestClassifier(n_estimators=n_estimator)       rf.fit(X[training], y[training])       confusion_matrixes[n_estimator] = confusion_matrix(y[~training],                                         rf.predict(X[~training]))
                                         
accuracy = lambda x: np.trace(x) / np.sum(x, dtype=float)confusion_matrixes[n_estimator] =                         accuracy(confusion_matrixes[n_estimator])accuracy_series = pd.Series(confusion_matrixes)import itertoolsfrom matplotlib import pyplot as pltf, ax = plt.subplots(figsize=(7, 5))accuracy_series.plot(kind='bar', ax=ax, color='k', alpha=.75)ax.grid()ax.set_title("Accuracy by Number of Estimators")ax.set_ylim(0, 1) # we want the full scopeax.set_ylabel("Accuracy")ax.set_xlabel("Number of Estimators")
```

## Support Vector Machine

```python
from sklearn import datasetsX, y = datasets.make_classification()
from sklearn.svm import SVCbase_svm = SVC()base_svm.fit(X, y)
```

## Decision Tree Classifier

```python
from sklearn import datasetsX, y = datasets.make_classification(n_samples=10000, n_classes=3,
		n_informative=3)from sklearn.tree import DecisionTreeClassifierdt = DecisionTreeClassifier()dt.fit(X, y)dt.predict(X)--> array([1, 1, 0, .., 2, 1, 1])
```




```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.cross_validation import train_test_split
# Training a RF to get some metrics
X_train, X_val, y_train, y_val = train_test_split(train, train_outcome, test_size=0.1)
forest = RandomForestClassifier(n_estimators=250, n_jobs=2)
forest.fit(X_train, y_train)
y_pred_val = forest.predict(X_val)
from sklearn.metrics import classification_report, accuracy_score
print(classification_report(y_val, y_pred_val))
print(accuracy_score(y_val, y_pred_val))
# Training a RF with the complete training set
forest = RandomForestClassifier(n_estimators=500, n_jobs=2)
forest.fit(train, train_outcome)
y_pred = forest.predict_proba(test)
```

(<a href="#top">Back to top</a>)
<hr>



# Support Vector machine
```python
from sklearn.svm import SVC
model = SVC(kernel='linear')
model = model.fit(train_data[0:,2:], train_data[0:,0])
```

(<a href="#top">Back to top</a>)
<hr>
