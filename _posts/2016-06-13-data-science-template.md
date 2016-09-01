---
title: "Data science template"
description: ""
category: datascience
tags: [datascience]
sidebar:
  nav: "new_side"
---


This serves as a template for data science tasks/challenges in (R and python)

The idea is that this template allows me to walk through the most important steps of doing a successful data science project.

It is very much work in progress and will be regularly updated.


![http://api.ning.com/files/h-Z9hSNEhWC5616zL-0TutSMaEA38-qlHEUVm0op4UN0MZBxZvcPgBWnmKbwuycLqzEYFZSNlo*qpqegs2SZkTa0fVy1vUh*/4.jpeg](http://api.ning.com/files/h-Z9hSNEhWC5616zL-0TutSMaEA38-qlHEUVm0op4UN0MZBxZvcPgBWnmKbwuycLqzEYFZSNlo*qpqegs2SZkTa0fVy1vUh*/4.jpeg)


### Table of contents

* TOC
{:toc}





# Data import/export
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


# Python reference

* <a href="https://gist.github.com/decc949d91162dc1a2183ebb3b281370">Imports</a>
* <a href="https://gist.github.com/4f304163997f6e81023884299d83d20f">Data types</a>
* <a href="https://gist.github.com/c7fd8b59aa843f0ae4fc10a10ec58229">I/O </a>
* <a href="https://gist.github.com/57d481588fc4fadb7d0c5a42525ca226">Strings</a>
* <a href="https://gist.github.com/475d844c4396fbb8ec205557387604ef">Sets</a>
* <a href="https://gist.github.com/1a05ba1d737fdd03ccf66f3d638f633f">Lists</a>
* <a href="https://gist.github.com/66749b841978bd9008357e10a0ebb563">Tuples</a>
* <a href="https://gist.github.com/83c696009b48389738a8b75f667693ce">Dictionary</a>
* <a href="https://gist.github.com/9ca009f3eb45f7d6ca987874cf7449f6">Conditional statement</a>
* <a href="https://gist.github.com/da99209a678715d0adadb57f9dfee69d">Comparison and boolean</a>
* <a href="https://gist.github.com/80ca194b513f3bd19673b161ceae3ba7">For loops</a>
* <a href="https://gist.github.com/11febad6aa5cc0c8804ee4f3eb02bd67">Functions</a>
* <a href="https://gist.github.com/5bf519867e3b34ce0772c8a9b8a9e424">Regex</a>
* <a href="https://gist.github.com/9689e7bb39984def6309c55735eed2e6">Exceptions</a>
* <a href="https://gist.github.com/f5136dd32b795c9576c0d74117f147db">Math</a>



