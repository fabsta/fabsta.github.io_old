---
title: "Data science template"
description: ""
category: DataScience
tags: [DataScience]
---



This serves as a template for data science tasks/challenges in (R and python)

The idea is that this template allows me to walk through the most important steps of doing a successful data science project.

It is very much work in progress and will be regularly updated.


![http://api.ning.com/files/h-Z9hSNEhWC5616zL-0TutSMaEA38-qlHEUVm0op4UN0MZBxZvcPgBWnmKbwuycLqzEYFZSNlo*qpqegs2SZkTa0fVy1vUh*/4.jpeg](http://api.ning.com/files/h-Z9hSNEhWC5616zL-0TutSMaEA38-qlHEUVm0op4UN0MZBxZvcPgBWnmKbwuycLqzEYFZSNlo*qpqegs2SZkTa0fVy1vUh*/4.jpeg)


### Table of contents

* TOC
{:toc}


# Preparation

## Clean IDE environment
*R*

```R
rm(list = ls())
```

*Python* 

```Python
---
```

<a href="#top">top</a>

___

## Loading packages

___

# Data import/exort
code gist (<a href="https://gist.github.com/b9c3e1182fc2b53e75fcb65f07aacc00">Python</a>,
<a href="https://gist.github.com/6535d6fe38eb542082c1ce7f286e52b2">R</a>,
<a href="https://gist.github.com/d6c97780f4a56f4115222b661b5053b4">Spark</a>)



___

# Preprocessing
common commands: class, str, summary, 


___
# Data exploration

code gist (<a href="https://gist.github.com/fabsta/d256ba38572629e30dbcb25e09d94ce0">Python</a>,
<a href="https://gist.github.com/fabsta/d256ba38572629e30dbcb25e09d94ce0">R</a>)


___


# Feature engineering/selection


gist (<a href="https://gist.github.com/f41bcdcbf107eaa5aec90464f0bef8e6">Python</a>,
<a href="https://gist.github.com/de0a0d8e5adab3ebbc27381dea1a4ccc">R</a>)

___

# Clean data - ignore IDs, outputs, missing


<a href="https://gist.github.com/cfd79f0b453b6310d53ce1160548905d">gist (python)</a><br>
<a href="https://gist.github.com/94f63d255f2e0c105bc3d30e42c9fc90">gist (R)</a>

___

# Building models

## Formula to describe the goal



## Modeling

### XGBoost

### RandomForest

### Assembling models


# Evaluation

### Confusion matrix

*R*

```
table(actual, cl.nb, dnn=c("Actual", "Predicted"))
```

*Python*

```Python
---
```
<a href="#top">top</a>

___

### ROC curves





<a href="#top">top</a>

___





# Save the dataset
*R*

```R
dsdate      <- paste0("_", format(Sys.Date(), "%y%m%d"))
dsrdata     <- paste0(dsname, dsdate, ".RData")
save(ds, dsname, dspath, dsdate, target, risk, id, ignore, vars,
     nobs, omit, inputi, inputc, numi, numc, cati, catc, file=dsrdata)
```
*Python*

```Python
---
```
<a href="#top">top</a>

___



