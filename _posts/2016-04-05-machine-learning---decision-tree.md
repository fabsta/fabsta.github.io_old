---
title: "Machine learning   Decision tree"
description: ""
category: 
tags: []
---


# Decision tree

Good introduction [slideshare link](http://www.slideshare.net/khusuma/decision-tree-and-random-forest).

Spark example [API](http://spark.apache.org/docs/latest/mllib-decision-tree.html).

## Example
![example picture of decision tree](http://web.fhnw.ch/personenseiten/taoufik.nouri/Data%20Mining/Course/Course3/DM-Par1.gif?raw=true)

## Node impurity
is a measure of homogeneity of labels at the node

* Gini impurity (Classification, [example]()) 
* Entropy (Classification)
* Variance (Regression)

Information gain:
Measures how well a given attribute separates the training examples according to their target classification (label).

Assuming that a split *s* partitions the dataset *D* of size *N* into two datasets *Dleft* and *Dright* of sizes *Nleft* and *Nright*, respectively, the information gain is:

IG(D,s) = Impurity(D) - Impurity(D_left) - Impurity(D_right)

## Entropy
E(S) = Sum -p * log * pi

## Information gain
E(T,X) = Sum

## How decision trees are built
Greedy algorithm that recursively splits tree. Each split is a binary partitioning of the feature space (e.g. age < 45).
Each partition is chosen by selecting the best split from set of possible splits.

Goal: Maximize information gain at tree node.


* step 1: Calculate entropy of feature
* step 2: Calculate information gain for each attribute
* step 3: Choose attribute with largest information gain as decision node
* step 4: a branch with entropy 0 is a leaf node
* step 4a: a branch with entropy > 0 needs further splitting
* step 5: continues recursively on inner nodes until all data is classified	


## Stopping rule
the algorithm stops when one of the following conditions is met


* node depth = defined maxDepth of training
* no split candidate leads to information gain > minInfoGain
* no split candidate produces child nodes with > minInstancePerNode training examples


## measuring accuracy
### binary classification 

precision = 

