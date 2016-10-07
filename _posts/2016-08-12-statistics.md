---
title: "Overview of common statistics concepts"
description: "Overview of common statistics concepts"
category: statistics, data science
tags: []
---

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

### Table of contents

* TOC
{:toc}


# Logarithm

The logit or log of the odds ratio is a logarithm, mapping the set of positive numbers onto the set of all real numbers. 

<img src="http://mathvault.ca/wp-content/uploads/Graphs-of-Different-Logarithms-534x400.png" width="600px">


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