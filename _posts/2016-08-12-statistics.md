---
title: "Overview of common statistics concepts"
description: "Overview of common statistics concepts"
category: datascience
tags: []
---

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

### Table of contents

* TOC
{:toc}

# Generative models

## Probabilities

### Joint probability

$$ p(X,Y) =  p (X and Y)   = p (X) * P(Y) $$

## Conditional probability

$$ p(Y|X) = \frac{P(Y,X)}{P(X)}  $$



## Bayes rule

$$  P(Y|X) = \frac{P(X|Y) * P(X)}{P(Y)}  $$

# Logarithm

The logit or log of the odds ratio is a logarithm, mapping the set of positive numbers onto the set of all real numbers. 

<img src="http://mathvault.ca/wp-content/uploads/Graphs-of-Different-Logarithms-534x400.png" width="600px">



# Unsupervised learning

## Clustering algorithms

### Kmeans clustering
Optimization algorithm. Tries to minimize total error defined as the total sum of distance

$$ min_{C_k} \sum_l^k \sum_{x_i from C_k} d(x_i,m_k)$$

#### Density of a cluster
Density of a cluster $C_j$ with a centroid $c_j$ as the inverse of the Euclidean distance between all members of each cluster and its mean:
$$ d(C_j) = \frac{1}{\sum_{x aus C_j} (x-c)^2} $$

#### Manhatten distance

$$ d(x,y)  = \sum \abs{x_i - y_i}$$

#### Euclidean distance

$$ d(x,y)  = \sum (x_i - y_i)^2$$

#### Cosine distance

$$ d(x,y) =  \frac{\sum x_i y_i}{(\sum x_i^2) \sum y_i^2}^{1/2} $$ 



### Spectral clustering

### Hierarchical clustering

### Expectation Maximization

1. E-step: Expectation of the maximum likelihood for the observed data by inferring the latent values
2. M-Step: The model features that maximize the expectation

## Dimension reduction

### Principal Component Analysis
Purpose is to transform the original set of features into a new set of ordered features by decreasing the order of variance. Original observations are transformed into a set of variables with lower degree of correlation.

### Linear Discriminant Analysis


# Supervised learning

## Generative

### Sequence

#### Markov process

#### Hidden Markov models

#### Markov random fields

### Random

#### Naive Bayes

#### Latent Dirichlet Allocation

#### Deep belief network


## Discriminative

### Continuous (Regression)

#### Linear regression

#### Logistic regression

### Discrete (Classification)

#### Neural networks

#### Support vector machines

#### Maximum Entropy

#### Decision Trees

#### Conditional Random Fields

#### Random Forests 


# Reinforcement learning

## Markov

### Model based

#### Iterative value

#### Iterative Policy

### Temporal Difference

#### Q-learning

#### SARSA

## Evolution

### Rules

#### Learning Classifiers

#### XCS

### Optimizer

#### Stochastic Gradient

#### Genetic Algorithm

# Linear models

## GLM
$$Y = b_0 + b_1 X_1 + b_2 X_2 + \ldots + b_n X_n + e$$

where the residual error  $$ e = Y - \hat{Y} $$

# Naive Bayes
Bayes' theorem: 
$$p(a|b) = \frac{p(C_k)p(x|C_k)}{p(x)}$$

or

$$ posterior = \frac{prior*likelihood}{evidence}$$



# Root mean squared error

$$ \sqrt{\frac{1}{n}\sum_{j=1}^n (y_j - \hat{y_j})^2} $$

# Optimization

## Gradient descent

Linear least squares function: 

$$ J(\Theta_0,\Theta_1) = \frac{1}{2m}\sum_{i=1}^m (h(x_{t,i}) - y)^2 $$ 