---
title: "Data Science   Questions and Answers"
description: "List of data science questions and answers"
category: DataScience
tags: [DataScience, MachineLearning]
---


With this list I am trying to capture interesting questions on my journey to understand data science. The main purpose is to have an easy way to lookup common data science questions. 
Since they might be useful for others as well, I have put them on github.

Each question has an answer with reference and pictures in case I could find a good one.

The content will be updated regularly.


Current count of questions: 88 (06.08.2016)

### Table of contents

* TOC
{:toc}



## Data mining

### What does CRISP-DM mean?

Cross Industry Standard Process for Data Mining, commonly known by its acronym CRISP-DM, was a data mining process model that describes commonly used approaches that data mining experts use to tackle problems.

* Business Understanding: What should be accomplished from a business perspective

* Data Understanding: Acquiring the data needed to accomplish the objective

* Data Preparation: Selecting and cleaning the data. May transform/aggregate for analysis

* Modeling: Selecting technique, building and training the model, assessding accuracy

* Evaluation: Does the model meet business objectives

* Deployment: Strategy for deploying the model

<img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/CRISP-DM_Process_Diagram.png" width="1000px">

([picture source](https://upload.wikimedia.org/wikipedia/commons/b/b9/CRISP-DM_Process_Diagram.png))

(<a href="#top">Back to top</a> \| [source](https://en.wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining))


### What could a data mining process look like?
![https://www.safaribooksonline.com/library/view/predictive-analytics-and/9780128014608/IMAGES/B9780128014608000021/main.assets/f02-02-9780128014608.jpg](https://www.safaribooksonline.com/library/view/predictive-analytics-and/9780128014608/IMAGES/B9780128014608000021/main.assets/f02-02-9780128014608.jpg)


(<a href="#top">Back to top</a> \| [picture source](https://www.safaribooksonline.com/library/view/predictive-analytics-and/9780128014608/IMAGES/B9780128014608000021/main.assets/f02-02-9780128014608.jpg))

### How can you handle noisy data?

* Binning method: first sort the data and partition into (equi-depth) bins. Then one can smooth by bin means, bin median, bin boundaries
* Clustering: detect and remove outliers
* Expert knowledge: models detect potential outliers and they are validated by subject matter expert


## DataPreparation

### What are possible ways to deal with missing data?

There is no blanket answer to this question. It depends on your data and what you are doing with it. Here are some possible solutions (they have advantages/disadvantages):

* Use the feature’s mean value from all the available data.* Fill in the unknown with a special value like -1.* Ignore the instance.* Use a mean value from similar items.* Use another machine learning algorithm to predict the value.

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>

## Programming

### Python or R – Which one would you prefer for text analytics?

The best possible answer for this would be Python because it has Pandas library that provides easy to use data structures and high performance data analysis tools. 

(<a href="#top">Back to top</a> \| [source](https://www.dezyre.com/article/100-data-science-interview-questions-and-answers-general-for-2016/184))

<hr>

## General

### What are the different types 
![http://stackoverflow.com/questions/6879596/why-is-the-python-csv-reader-ignoring-double-quoted-fields](http://stackoverflow.com/questions/6879596/why-is-the-python-csv-reader-ignoring-double-quoted-fields)

(<a href="#top">Back to top</a> \| [source](http://thefinancialbrand.com/59805/banking-data-predictive-advanced-analytics/))


### What is a probability distribution?
A probability distribution assigns a probability to each measurable subset of the possible outcomes of a random experiment, survey, or procedure of statistical inference. 

(<a href="#top">Back to top</a> \| [source](https://en.wikipedia.org/wiki/Probability_distribution))

<hr>

### What types of probability distributions do you know?

![](http://blog.cloudera.com/wp-content/uploads/2015/12/distribution.png) 
(<a href="#top">Back to top</a> \| [picture source](http://blog.cloudera.com/wp-content/uploads/2015/12/distribution.png))
 
<hr>
 
### What do you understand by the term Normal Distribution?

Data is usually distributed in different ways with a bias to the left or to the right or it can all be jumbled up. However, there are chances that data is distributed around a central value without any bias to the left or right and reaches normal distribution in the form of a bell shaped curve. The random variables are distributed in the form of an asymmetrical bell shaped curve

![https://s3.amazonaws.com/files.dezyre.com/images/blog/100+Data+Science+Interview+Questions+and+Answers+(General)/Bell+Shaped+Curve+for+Normal+Distribution.jpg](https://s3.amazonaws.com/files.dezyre.com/images/blog/100+Data+Science+Interview+Questions+and+Answers+(General)/Bell+Shaped+Curve+for+Normal+Distribution.jpg) 

(<a href="#top">Back to top</a> \| [picture source](https://s3.amazonaws.com/files.dezyre.com/images/blog/100+Data+Science+Interview+Questions+and+Answers+(General)/Bell+Shaped+Curve+for+Normal+Distribution.jpg))

<hr>

### Differentiate between univariate, bivariate and multivariate analysis.

![http://image.slidesharecdn.com/quantitativedataanalysis-131122004449-phpapp01/95/quantitative-data-analysis-5-638.jpg?cb=1427965440](http://image.slidesharecdn.com/quantitativedataanalysis-131122004449-phpapp01/95/quantitative-data-analysis-5-638.jpg?cb=1427965440)

(<a href="#top">Back to top</a> \| [picture source](http://image.slidesharecdn.com/quantitativedataanalysis-131122004449-phpapp01/95/quantitative-data-analysis-5-638.jpg?cb=1427965440))

<hr>

### What is regularization and why it is useful?

Regularization is the process of adding a tuning parameter to a model to induce smoothness in order to prevent overfitting. 

This is most often done by adding a constant multiple to an existing weight vector. This constant is often either the L1 (Lasso) or L2 (ridge), but can in actuality can be any norm. The model predictions should then minimize the mean of the loss function calculated on the regularized training set. 


([source](http://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers.html))


![http://www.kdnuggets.com/images/regularization-lp-ball.jpg](http://www.kdnuggets.com/images/regularization-lp-ball.jpg)

(<a href="#top">Back to top</a> \| [picture source](http://www.kdnuggets.com/images/regularization-lp-ball.jpg))

<hr>

### What is overfitting? 

Overfitting is finding spurious results that are due to chance and cannot be reproduced by subsequent studies.

![http://i.stack.imgur.com/t0zit.png](http://i.stack.imgur.com/t0zit.png)

([picture source](http://i.stack.imgur.com/t0zit.png))

(<a href="#top">Back to top</a> \| [source](http://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers-part2.html))

<hr>

### How can you control for overfitting?

Several methods can be used to avoid "overfitting" the data

* Try to find the simplest possible hypothesis
* Regularization (adding a penalty for complexity)
* Randomization Testing (randomize the class variable, try your method on this data - if it find the same strong results, something is wrong)
* Nested cross-validation  (do feature selection on one level, then run entire method in cross-validation on outer level)
* Adjusting the [False Discovery Rate](http://en.wikipedia.org/wiki/False_discovery_rate)
* Using the [reusable holdout method](http://www.kdnuggets.com/2015/08/feldman-avoid-overfitting-holdout-adaptive-data-analysis.html) - a breakthrough approach proposed in 2015

<a href="#top">Back to top</a> 

<hr>

### What is the difference between bias and variance?

![http://blog.fliptop.com/wp-content/uploads/2015/01/Bias_Variance.jpg](http://blog.fliptop.com/wp-content/uploads/2015/01/Bias_Variance.jpg)

([picture source](http://blog.fliptop.com/wp-content/uploads/2015/01/Bias_Variance.jpg ))

(<a href="#top">Back to top</a> \| [picture source](http://blog.fliptop.com/wp-content/uploads/2015/01/Bias_Variance.jpg))

<hr>

### What is selection bias, why is it important?

Selection bias, in general, is a problematic situation in which error is introduced due to a non-random population sample. For example, if a given sample of 100 test cases was made up of a 60/20/15/5 split of 4 classes which actually occurred in relatively equal numbers in the population, then a given model may make the false assumption that probability could be the determining predictive factor.

<a href="#top">Back to top</a> 
<hr>
### How can you avoid selection bias?

Avoiding non-random samples is the best way to deal with bias; however, when this is impractical, techniques such as resampling, boosting, and weighting are strategies which can be introduced to help deal with the situation. 

<a href="#top">Back to top</a> 
<hr>
### What is oversampling and what is undersampling?

Oversampling means to duplicate samples, whereas undersampling means to delete samples. Oversampling might be used in cases where the number of positive samples is very limited, e.g. fraud detection.

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>

### What is the difference between "long" ("tall") and "wide" format data?

The problem is not just reshaping the data, but avoiding false positives by reducing the number of features to find most relevant ones. 

![http://www.kdnuggets.com/images/wide-data-tall-data.jpg](http://www.kdnuggets.com/images/wide-data-tall-data.jpg)

(<a href="#top">Back to top</a> \| [picture source](http://www.kdnuggets.com/images/wide-data-tall-data.jpg))

<hr>

## Visualization

### Explain Edward Tufte's concept of "chart junk."

Chart junk refers to all visual elements in charts and graphs that are not necessary to comprehend the information represented on the graph, or that distract the viewer from this information. 

The term chart junk was coined by Edward Tufte in his 1983 book The Visual Display of Quantitative Information. 

![http://www.exceluser.com/blogdata/images/post_001_133/chinacols.jpg](http://www.exceluser.com/blogdata/images/post_001_133/chinacols.jpg)


Here is a more modern example where it is very hard to understand the column plot because of workers and cranes that obscure them. 

[source](https://en.wikipedia.org/wiki/Chartjunk)

(<a href="#top">Back to top</a> \| 
[picture source](http://www.exceluser.com/blogdata/images/post_001_133/chinacols.jpg))

<hr>

## Natural language processing

### What is Natural Language Processing (NLP)
A Computer Science field connected to Artificial Intelligence and Computational Linguistics which focuses on interactions between computers and human language and a machine’s ability to understand, or mimic the understanding of human language. Examples of NLP applications include Siri and Google Now.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>


### What is Natural Language Processing (NLP)
A Computer Science field connected to Artificial Intelligence and Computational Linguistics which focuses on interactions between computers and human language and a machine’s ability to understand, or mimic the understanding of human language. Examples of NLP applications include Siri and Google Now.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>


### What is Information Extraction?
The process of automatically extracting structured information from unstructured and/or semi-structured sources, such as text documents or web pages for example.

![http://66.media.tumblr.com/e346cfd7bdd59cc21daca79299520bae/tumblr_inline_nnxs0lDdUA1sleek4_500.png](http://66.media.tumblr.com/e346cfd7bdd59cc21daca79299520bae/tumblr_inline_nnxs0lDdUA1sleek4_500.png)

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Named Entity Recognition (NER)?
The process of locating and classifying elements in text into predefined categories such as the names of people, organizations, places, monetary values, percentages, etc.


(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Corpus or Corpora?
A usually large collection of documents that can be used to infer and validate linguistic rules, as well as to do statistical analysis and hypothesis testing.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Sentiment Analysis?
The use of Natural Language Processing techniques to extract subjective information from a piece of text. i.e. whether an author is being subjective or objective or even positive or negative. (can also be referred to as Opinion Mining)

Sentiment Analysis:
![http://67.media.tumblr.com/829fcf76b557694b67c72f6f61b43476/tumblr_inline_nnxrxsJuZ21sleek4_500.png](http://67.media.tumblr.com/829fcf76b557694b67c72f6f61b43476/tumblr_inline_nnxrxsJuZ21sleek4_500.png)

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Word Sense Disambiguation?
The ability to identify the meaning of words in context in a computational manner. A third party corpus or knowledge base, such as WordNet or Wikipedia, is often used to cross-reference entities as part of this process. A simple example being, for an algorithm to determine whether a reference to “apple” in a piece of text refers to the company or the fruit.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Bag of Words?
A commonly used model in methods of Text Classification. As part of the BOW model, a piece of text (sentence or a document) is represented as a bag or multiset of words, disregarding grammar and even word order and the frequency or occurrence of each word is used as a feature for training a classifier.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Explicit Semantic Analysis (ESA)?
Used in Information Retrieval, Document Classification and Semantic Relatedness calculation (i.e. how similar in meaning two words or pieces of text are to each other), ESA is the process of understanding the meaning of a piece text, as a combination of the concepts found in that text.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Latent Semantic Analysis (LSA)?
The process of analyzing relationships between a set of documents and the terms they contain. Accomplished by producing a set of concepts related to the documents and terms. LSA assumes that words that are close in meaning will occur in similar pieces 
of text.

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>

### What is Latent Dirichlet Allocation (LDA)?
A common topic modeling technique, LDA is based on the premise that each document or piece of text is a mixture of a small number of topics and that each word in a document is attributable to one of the topics. 

(<a href="#top">Back to top</a> \| 
[source](http://blog.aylien.com/post/118289638578/10-common-nlp-terms-explained-for-the-text))

<hr>


### Principal component analysis





## MachineLearning


## Text mining

### What is the bag of words model?

In the bag of words model, a text (such as a sentence or a document) is represented as the bag (multiset) of its words, disregarding grammar and even word order but keeping multiplicity. 

The bag-of-words model is commonly used in methods of document classification, where the (frequency of) occurrence of each word is used as a feature for training a classifier. 

([source](https://en.wikipedia.org/wiki/Bag-of-words_model))

![http://image.slidesharecdn.com/irmaster-150830120759-lva1-app6892/95/ir-16-638.jpg](http://image.slidesharecdn.com/irmaster-150830120759-lva1-app6892/95/ir-16-638.jpg)

(<a href="#top">Back to top</a> \| [picture source](http://image.slidesharecdn.com/irmaster-150830120759-lva1-app6892/95/ir-16-638.jpg))

<hr>


## Search methods

### What is gradient ascent?

Gradient ascent is an optimization algorithm. It is based on the idea that if we want to find the maximum point on a function, then the best way to move is in the direction of the gradient.
One takes steps proportional to the positive of the gradient (or of the approximate gradient) of the function at the current point. 
E.g. one could use gradient ascent to find the best weights for a logistic regression classifier.

([source](https://www.manning.com/books/machine-learning-in-action))

![https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Gradient_descent.svg/350px-Gradient_descent.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Gradient_descent.svg/350px-Gradient_descent.svg.png)

(<a href="#top">Back to top</a> \| [picture source](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Gradient_descent.svg/350px-Gradient_descent.svg.png))

<hr>

### What is the difference between gradient ascent and gradient descent?

Both gradient descent and ascent are practically the same.
Typically, you'd use gradient ascent to maximize a likelihood function, and gradient descent to minimize a cost function.  

![http://image.slidesharecdn.com/pkfetdxyqpiy2i94fvzv-signature-25ed596523f4a669f9a710899d8eaf303c4bbdce8b8e80e99e004c3f91b28bcc-poli-151222094839/95/recommender-systems-50-638.jpg?cb=1450777740](http://image.slidesharecdn.com/pkfetdxyqpiy2i94fvzv-signature-25ed596523f4a669f9a710899d8eaf303c4bbdce8b8e80e99e004c3f91b28bcc-poli-151222094839/95/recommender-systems-50-638.jpg?cb=1450777740)

(<a href="#top">Back to top</a> \| [source](http://stackoverflow.com/questions/22594063/what-is-the-difference-between-gradient-descent-and-gradient-ascent))

<hr>

### What is the difference between gradient ascent and stochastic gradient ascent?

Gradient ascent uses all data points on each update.
Stochastic gradient ascent only uses one instance at a time.

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>

### What is a general approach for k-nearest neighbors?

General approach to kNN1. Collect: Any method.2. Prepare: Numeric values are needed for a distance calculation. A structured data format is best.3. Analyze: Any method.4. Train: Does not apply to the kNN algorithm.5. Test: Calculate the error rate.6. Use: This application needs to get some input data and output structured num- eric values. Next, the application runs the kNN algorithm on this input data and determines which class the input data should belong to. The application then takes some action on the calculated class. 

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>



### What is the diffeence between classification and regression?

Regression is used to predict continuous values. 
Classification is used to predict which class a data point is part of (discrete value). 

Example: I have a house with W rooms, X bathrooms, Y square-footage and Z lot-size. Based on other houses in the area that have recently sold, how much (dollar amount) can I sell my house for? I would use regression for this kind of problem. 

Example: I have an unknown fruit that is yellow in color, 5.5 inches long, diameter of an inch, and density of X. What fruit is this? I would use classification for this kind of problem to classify it as a banana (as opposed to an apple or orange). 

([source](https://www.quora.com/What-is-the-main-difference-between-classification-problems-and-regression-problems-in-machine-learning))

![http://ipython-books.github.io/images/ml.png](http://ipython-books.github.io/images/ml.png)

(<a href="#top">Back to top</a> \| [picture source](http://ipython-books.github.io/images/ml.png))

<hr>

## Regression analysis

### What is a gerneal approach to regression?

General approach to regression1. Collect: Any method.2. Prepare: We’ll need numeric values for regression. Nominal values should be mapped to binary values.3. Analyze: It’s helpful to visualized 2D plots. Also, we can visualize the regression weights if we apply shrinkage methods.4. Train: Find the regression weights.5. Test: We can measure the R2, or correlation of the predicted value and data, to measure the success of our models.6. Use: With regression, we can forecast a numeric value for a number of inputs. This is an improvement over classification because we’re predicting a continu- ous value rather than a discrete category.

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>

### What is Linear Regression?

In statistics, linear regression is an approach for modeling the relationship between a scalar dependent variable y and one or more explanatory variables (or independent variables) denoted X. The case of one explanatory variable is called simple linear regression. 

(<a href="#top">Back to top</a> \| [source](https://www.google.at/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwiy19vJ5JDMAhVEOhQKHcmOCfcQFggkMAI&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FLinear_regression&usg=AFQjCNElrDTjzTcTHtgto2sw_hah27cmjg&bvm=bv.119408272,bs.1,d.bGg))

### What is the difference between multiple linear regression and multivariate linear regression?

Multiple linear regression has >1 explanatory variable (input), whereas multivariate linear regression predicts multiple correlated depentend variables. 

(<a href="#top">Back to top</a> \| [source](https://en.wikipedia.org/wiki/Linear_regression))

<hr>




### What is logistic regression?

Logistic regression is a statistical method for analyzing a dataset in which there are one or more independent variables that determine an outcome. The outcome is measured with a dichotomous variable (in which there are only two possible outcomes).

![https://www.mssqltips.com/tipimages2/3471_Example.JPG](https://www.mssqltips.com/tipimages2/3471_Example.JPG)

(<a href="#top">Back to top</a> \| [picture source](https://www.mssqltips.com/tipimages2/3471_Example.JPG))

<hr>

### What is a general approach to logistic regression?

General approach to logistic regression1. Collect: Any method.2. Prepare: Numeric values are needed for a distance calculation. A structured data format is best.3. Analyze: Any method.4. Train: We’ll spend most of the time training, where we try to find optimal coefficients to classify our data.5. Test: Classification is quick and easy once the training step is done.6. Use: This application needs to get some input data and output structured numeric values. Next, the application applies the simple regression calculation on this input data and determines which class the input data should belong to. The application then takes some action on the calculated class.

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>



### What are shrinkage methods?

Regressions can be done for any dataset provided that given an input matrix X we can compute the inverse of XtX.
There are two situations where you can't compute the inverse. If you have

* more features than data points
* more data points than features and features are highly correlated.


Shrinkage methods allow to compute regression coefficients without being able to compute the inverse of XtX. Shrinkage methods impose a constraint on the size of the regression coefficient. They allow to throw out unimportant parameters.

Popular shrinkage methods are:

* Ridge regression
* Lasso regression
* Forward stagewise regression

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>

### What is the ridge in ridge regression?Ridge regression uses the identity matrix multiplied by some constant . If you look at I (the identity matrix), you’ll see that there are 1s across the diagonal and 0s elsewhere. This ridge of 1s in a plane of 0s gives you the ridge in ridge regression.

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>


### What is a general approach to tree-based regression?

General approach to tree-based regression
1. Collect: Any method.2. Prepare: Numeric values are needed. If you have nominal values, it’s a good idea to map them into binary values.3. Analyze: We’ll visualize the data in two-dimensional plots and generate trees as dictionaries.4. Train: The majority of the time will be spent building trees with models at the leaf nodes.5. Test: We’ll use the R2 value with test data to determine the quality of our models.6. Use: We’ll use our trees to make forecasts. We can do almost anything with these results.

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>


## Naive Bayes
### Why is naive Bayesian classification called naive?

Naive Bayesian Classification (NBC) isreferred to as naive since it makes tha assumption that each of its inputs are independent of each other, an assumption which rarely holds true, and hence the word naive. Research has however shown that even though this assumption is often false, the technique still performs well, and hence NBC is seen as a simple yet powerful tool in the world of classification and machine learning. 

(<a href="#top">Back to top</a> \| [source](http://www.answers.com/Q/Why_is_naive_Bayesian_classification_called_naive))

<hr>

### What is a general approach to naive Bayes?

General approach to naïve Bayes
1. Collect: Any method. We’ll use RSS feeds in this chapter.2. Prepare: Numeric or Boolean values are needed.3. Analyze: With many features, plotting features isn’t helpful. Looking at histo- grams is a better idea.4. Train: Calculate the conditional probabilities of the independent features.5. Test: Calculate the error rate.6. Use: One common application of naïve Bayes is document classification. You can use naïve Bayes in any classification setting. It doesn’t have to be text. 

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>



## Clustering

### What is a general approach to K-means clustering?

General approach to k-means clustering
1. Collect: Any method.2. Prepare: Numeric values are needed for a distance calculation, and nominal val- ues can be mapped into binary values for distance calculations.3. Analyze: Any method.4. Train: Doesn’t apply to unsupervised learning.5. Test: Apply the clustering algorithm and inspect the results. Quantitative error measurements such as sum of squared error (introduced later) can be used.6. Use: Anything you wish. Often, the clusters centers can be treated as represen- tative data of the whole cluster to make decisions.


(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))
<hr>

## Support Vector machines

### What is a general approach to Support Vector machines?

General approach to SVMs1. Collect: Any method.2. Prepare: Numeric values are needed.3. Analyze: It helps to visualize the separating hyperplane.4. Train: The majority of the time will be spent here. Two parameters can be adjusted during this phase.5. Test: Very simple calculation.6. Use: You can use an SVM in almost any classification problem. One thing to note is that SVMs are binary classifiers. You’ll need to write a little more code to use an SVM on a problem with more than two classes.

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>

### What means linearly separable and what is a separating hyperplane?
If you have two groups of data, and the data points are sep- arated enough that you could draw a straight line with all the points of one class on one side of the line and all the points of the other class on the other side of the line. This line is called separating hyperplane.

([source](https://www.manning.com/books/machine-learning-in-action))

![http://www.statistics4u.info/fundstat_eng/img/hl_classif_separation.png](http://www.statistics4u.info/fundstat_eng/img/hl_classif_separation.png)

(<a href="#top">Back to top</a> \| [picture source](http://www.statistics4u.info/fundstat_eng/img/hl_classif_separation.png))

<hr>

### What does the “support” mean in Support Vector Machine?

"In SVMs the resulting separating hyper-plane is attributed to a sub-set of data feature vectors (i.e., the ones that their associated Lagrange multipliers are greater than 0). These feature vectors were named support vectors because intuitively you could say that they "support" the separating hyper-plane or you could say that for the separating hyper-plane the support vectors play the same role as the pillars to a building."


(<a href="#top">Back to top</a> \| [source](http://stackoverflow.com/questions/21694855/what-does-the-support-mean-in-support-vector-machine?rq=1))

<hr>

### What is the difference between hard margin linear SVM and soft margin linear SVM?

If the data is linearly separable, you can use a hard margin (no slack allowed). The support vectors lie exactly on the margin. Regardless of the number of dimensions or size of data set, the number of support vectors could be as little as 2.

![https://upload.wikimedia.org/wikipedia/commons/2/2a/Svm_max_sep_hyperplane_with_margin.png](https://upload.wikimedia.org/wikipedia/commons/2/2a/Svm_max_sep_hyperplane_with_margin.png)

[picture source](https://upload.wikimedia.org/wikipedia/commons/2/2a/Svm_max_sep_hyperplane_with_margin.png)

If the data is not linearly separable, we relax our constraint that no data points may lie outside the margin. So, we allow some amount of them to stray over the line into the margin. This amount is controlled by the slack parameter C. This gives a wider margin (+ greater error), but improves generalization and to find linear separation of linearly inseparable data.

([source](http://stackoverflow.com/questions/9480605/what-is-the-relation-between-the-number-of-support-vectors-and-training-data-and?rq=1))


![http://i.stack.imgur.com/npEOk.png](http://i.stack.imgur.com/npEOk.png) 

(<a href="#top">Back to top</a> \| [picture source](http://i.stack.imgur.com/npEOk.png))

<hr>

### What is a kernel-method?

Kernel methods allow linear SVM to learn nonlinear decision boundaries. This is done by replacing all dot products with a kernel function (aka kernel trick). We can now work in higher dimensional space.
They are basically a mapping of one feature space to another.

(<a href="#top">Back to top</a> \| [source](http://www.eric-kim.net/eric-kim-net/posts/1/kernel_trick.html))

<hr>


## Decision trees

### What is tree pruning and what is it good for?

Trees with too many nodes are an example of a model overfit to the data. Cross-validation can be used to find out if we're overfitting the data. 
Reducing the complexity of a decision trees to avoid overfitting is called *pruning*. Less informative subtree will be cut away.

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>
### What is a general approach for decision trees?

General approach to decision trees1. Collect: Any method.2. Prepare: This tree-building algorithm works only on nominal values, so any contin- uous values will need to be quantized.3. Analyze: Any method. You should visually inspect the tree after it is built.4. Train: Construct a tree data structure.5. Test: Calculate the error rate with the learned tree.6. Use: This can be used in any supervised learning task. Often, trees are used to better understand the data. 

(<a href="#top">Back to top</a> \| [source](https://www.manning.com/books/machine-learning-in-action))

<hr>




## Ensembl learning



### How do ensembl methods work?
There are three broad classes of ensemble algorithms:

* Bagging– Random Forests are in this group
* Boosting
* Stacking

The idea behind ensembles is straightforward.  Using multiple models and combining their results generally increases the performance of a model or at least reduces the probability of selecting a poor one.  One of the most interesting implications of this is that the ensemble model may in fact not be better than the most accurate single member of the ensemble, but it does reduce the overall risk. 
There are a number of strategies for combining single predictors into ensembles represented by the three major groups above and lots of detailed variation among implementations even within these groups.  Despite the warning that ensembles can actually only guarantee to reduce risk, most of us have experienced that our most accurate models are in fact ensembles.

![http://api.ning.com/files/wrR3Z9xe9sJq990CffTVJP9ybHkxezcp8wahDWYxsRibma25ni*N4AUCGG7KEkglFLEwD8mdCW7XMxVNZTuh05ktVnRZBPmi/Combining_classifiers2.jpg](http://api.ning.com/files/wrR3Z9xe9sJq990CffTVJP9ybHkxezcp8wahDWYxsRibma25ni*N4AUCGG7KEkglFLEwD8mdCW7XMxVNZTuh05ktVnRZBPmi/Combining_classifiers2.jpg)

(<a href="#top">Back to top</a> \| [source](([source](http://www.datasciencecentral.com/profiles/blogs/want-to-win-at-kaggle-pay-attention-to-your-ensembles?overrideMobileRedirect=1))))
<hr>


### How would you compare Bagging and boosting?

#### Bagging (Bootstrap Aggregating)

Popular Tool:  Random Forest

Concept:  Bagging is perhaps the earliest ensemble technique being credited to Leo Brieman at Berkeley in 1996.  It trains and selects a group of strong learners on bootstapped subsets of data and yields its result by simple plurality of voting.
Originally it was designed for decision trees but it works equally well with other unstable classifier types such as neural nets.

Strengths:

* Robust against outliers and noise. 
* Reduces variance and typically avoids overfitting.
* Easy to use with limited well established default parameters.  Works well off the shelf requiring little additional tuning. 
* Fast run time.
* Since it is tree based it confers most of the advantages of trees like handling missing values, automatic selection of variable importance, and accomodating highly non-linear interactions.

Weakness:

* Can be slow to score as complexity increases.
* Lack of transparancy due to the complexity of multiple trees.
 
#### Boosting
Popular Tools: Adaboost, Gradient Boosted Models (GBM). 

Concept:  Similar to Bagging but with an emphasis on improving weak learners.  Each iteration of boosting creates three weak classifiers.  The first classifier is trained normally on a subset of the data.  The second classifier is trained on data in which the first classifier achieved only 50% correct identification.  The third classifier is trained on data for which the first and second classifier disagree.  The three classifiers are combined through a simple majority vote.
Adaboost and GBM are quite similar except in the way they deal with their loss functions.

Strengths:

* Often the best possible model.
* Directly optimizes the cost function.

Weaknesses

* Not robust against outliers and noise.
* Can overfit.
* Need to find proper stopping point.
* Several hyper-parameters.
* Lack of transparancy due to the complexity of multiple trees.


#### Comparing Bagging and Boosted Methods

Model error arises from noise, bias, and variance.

* Noise is error by the target function.
* Bias is where the algorithm cannot learn the target.
* Variance comes from sampling.

Bagging is not recommended on models that have a high bias. Boosting is recommended for high bias.
Conversely Boosting is not recommended for cases of high variance.  Bagging is recommended for high variance.
Both techniques can effectively deal with noise.


(<a href="#top">Back to top</a> \| [source](([source](http://www.datasciencecentral.com/profiles/blogs/want-to-win-at-kaggle-pay-attention-to-your-ensembles?overrideMobileRedirect=1))))
<hr>

### What is a general approach to AdaBoost?

General approach to AdaBoost1. Collect: Any method.2. Prepare: It depends on which type of weak learner you’re going to use. In this chapter, we’ll use decision stumps, which can take any type of data. You could use any classifier, so any of the classifiers from chapters 2–6 would work. Simple classifiers work better for a weak learner.3. Analyze: Any method.4. Train: The majority of the time will be spent here. The classifier will train the weak learner multiple times over the same dataset.5. Test: Calculate the error rate.6. Use: Like support vector machines, AdaBoost predicts one of two classes. If you want to use it for classification involving more than two classes, then you’ll need to apply some of the same methods as for support vector machines.

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>


## Time Series


### How to check stationarity of a Time Series?

A time series (TS) is said to be stationary if its statistical properties such as mean, variance remain constant over time. But why is it important? Most of the TS models work on the assumption that the TS is stationary. Intuitively, we can sat that if a TS has a particular behaviour over time, there is a very high probability that it will follow the same in the future. Also, the theories related to stationary series are more mature and easier to implement as compared to non-stationary series.

Stationarity is defined using very strict criterion. However, for practical purposes we can assume the series to be stationary if it has constant statistical properties over time, ie. the following:

* constant mean
* constant variance
* an autocovariance that does not depend on time.


We can check stationarity using the following:

* Plotting Rolling Statistics: We can plot the moving average or moving variance and see if it varies with time. By moving average/variance I mean that at any instant ‘t’, we’ll take the average/variance of the last year, i.e. last 12 months. But again this is more of a visual technique.

* Dickey-Fuller Test: This is one of the statistical tests for checking stationarity. Here the null hypothesis is that the TS is non-stationary. The test results comprise of a Test Statistic and some Critical Values for difference confidence levels. If the ‘Test Statistic’ is less than the ‘Critical Value’, we can reject the null hypothesis and say that the series is stationary. Refer [this article](http://www.analyticsvidhya.com/blog/2015/12/complete-tutorial-time-series-modeling/) for details.


Further reading: [http://www.analyticsvidhya.com/blog/2015/12/complete-tutorial-time-series-modeling/](http://www.analyticsvidhya.com/blog/2015/12/complete-tutorial-time-series-modeling/)


(<a href="#top">Back to top</a> \| [source](http://www.analyticsvidhya.com/blog/2016/02/time-series-forecasting-codes-python/))

<hr>

### What makes a Time Series non-stationary?


There are 2 major reasons behind non-stationaruty of a TS:

1. Trend – varying mean over time. For eg, in this case we saw that on average, the number of passengers was growing over time.
2. Seasonality – variations at specific time-frames. eg people might have a tendency to buy cars in a particular month because of pay increment or festivals.


(<a href="#top">Back to top</a> \| [source](http://www.analyticsvidhya.com/blog/2016/02/time-series-forecasting-codes-python/))

<hr>


### What is the exponential smoothing model (time series)?

Exponential smoothing models use weights for past observations, such as a moving average model, but unlike moving average models, the more recent the observation, the more weight it is given, relative to the later ones. There are three possible smoothing parameters to estimate: the overall smoothing parameter, a trend parameter, and smoothing parameter. If no trend or seasonality is present, then these parameters become null.



(<a href="#top">Back to top</a> \| [source](https://www.safaribooksonline.com/library/view/mastering-machine-learning/9781783984527/ch11.html))

<hr>


## Evaluation of Classification Models

### What is cross-validation?

Cross-validation, sometimes called rotation estimation, is a model validation technique for assessing how the results of a statistical analysis will generalize to an independent data set.

([source](https://en.wikipedia.org/wiki/Cross-validation_(statistics)))

![http://blog-test.goldenhelix.com/wp-content/uploads/2015/04/B-fig-1.jpg](http://blog-test.goldenhelix.com/wp-content/uploads/2015/04/B-fig-1.jpg)

(<a href="#top">Back to top</a> \| [picture source](http://blog-test.goldenhelix.com/wp-content/uploads/2015/04/B-fig-1.jpg))

<hr>

### What is an advantage of using cross-validation over conventional validation (70%/30%)?

One of the main reasons for using cross-validation instead of using the conventional validation (e.g. partitioning the data set into two sets of 70% for training and 30% for test) is that the error (e.g. Root Mean Square Error) on the training set in the conventional validation is not a useful estimator of model performance and thus the error on the test data set does not properly represent the assessment of model performance. This may be because there is not enough data available or there is not a good distribution and spread of data to partition it into separate training and test sets in the conventional validation method. In these cases, a fair way to properly estimate model prediction performance is to use cross-validation as a powerful general technique. 

(<a href="#top">Back to top</a> \| [source](https://en.wikipedia.org/wiki/Cross-validation_(statistics)))

<hr>


### Explain what precision and recall are. How do they relate to the ROC curve?


Calculating precision and recall is actually quite easy. Imagine there are 100 positive cases among 10,000 cases. You want to predict which ones are positive, and you pick 200 to have a better chance of catching many of the 100 positive cases.  You record the IDs of your predictions, and when you get the actual results you sum up how many times you were right or wrong. There are four ways of being right or wrong:

1. TN / True Negative: case was negative and predicted negative
2. TP / True Positive: case was positive and predicted positive
3. FN / False Negative: case was positive but predicted negative
4. FP / False Positive: case was negative but predicted positive

Makes sense so far? Now you count how many of the 10,000 cases fall in each bucket, say:

|                | Predicted Negative | Predicted Positive |
|----------------|--------------------|--------------------|
| Negative Cases | TN: 9,760          | FP: 140            |
| Positive Cases | FN: 40             | TP: 60             |

Now, your boss asks you three questions:

* What percent of your predictions were correct? 
  You answer: the "accuracy" was (9,760+60) out of 10,000 = 98.2%
* What percent of the positive cases did you catch? 
You answer: the "recall" was 60 out of 100 = 60%
* What percent of positive predictions were correct? 
You answer: the "precision" was 60 out of 200 = 30%


![http://www.kdnuggets.com/images/precision-recall-relevant-selected.jpg](http://www.kdnuggets.com/images/precision-recall-relevant-selected.jpg)

(<a href="#top">Back to top</a> \| [picture source](http://www.kdnuggets.com/images/precision-recall-relevant-selected.jpg))

<hr>



### What is a confusion matrix?

In the field of machine learning and specifically the problem of statistical classification, a confusion matrix, also known as an error matrix, is a specific table layout that allows visualization of the performance of an algorithm, typically a supervised learning one (in unsupervised learning it is usually called a matching matrix). Each column of the matrix represents the instances in a predicted class while each row represents the instances in an actual class (or vice-versa). The name stems from the fact that it makes it easy to see if the system is confusing two classes (i.e. commonly mislabeling one as another).

[https://en.wikipedia.org/wiki/Confusion_matrix](https://en.wikipedia.org/wiki/Confusion_matrix)

![http://3.bp.blogspot.com/_txFWHHNYMJQ/THyADzbutYI/AAAAAAAAAf8/TAXL7lySrko/s1600/Picture+8.png](http://3.bp.blogspot.com/_txFWHHNYMJQ/THyADzbutYI/AAAAAAAAAf8/TAXL7lySrko/s1600/Picture+8.png)

(<a href="#top">Back to top</a> \| [picture source](http://3.bp.blogspot.com/_txFWHHNYMJQ/THyADzbutYI/AAAAAAAAAf8/TAXL7lySrko/s1600/Picture+8.png))

<hr>


### What is statistical power?

Wikipedia defines Statistical power or sensitivity of a binary hypothesis test is the probability that the test correctly rejects the null hypothesis (H0) when the alternative hypothesis (H1) is true. 

To put in another way, Statistical power is the likelihood that a study will detect an effect when the effect is present. The higher the statistical power, the less likely you are to make a Type II error (concluding there is no effect when, in fact, there is). 

(<a href="#top">Back to top</a> \| [source](http://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers.html/3))

<hr>




## Applications

### Recommendation engine
#### What is a recommendation engine?

Recommendation Engines are a subclass of information filtering system that seek to predict the ‘rating’ or ‘preference’ that user would give to an item.

(<a href="#top">Back to top</a>)

<hr>

#### How does a recommendation engine work?

They typically produce recommendations in one of two ways: using collaborative or content-based filtering. 

* Collaborative filtering methods build a model based on users past behavior (items previously purchased, movies viewed and rated, etc) and use decisions made by current and other users. This model is then used to predict items (or ratings for items) that the user may be interested in. 

* Content-based filtering methods use features of an item to recommend additional items with similar properties. These approaches are often combined in Hybrid Recommender Systems.  

(<a href="#top">Back to top</a> \| [source](http://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers-part2.html/3))
<hr>



## Unsorted

### What is classification imbalance?

Occurs when we’re trying to classify items but don’t have an equal number of examples. 
Detecting fraudulent credit card use is a good example of this: we may have 1,000 negative examples for every positive example.

![http://sci2s.ugr.es/sites/default/files/files/ComplementaryMaterial/imbalanced/yeast4_s1.0tr_mcg_vs_gvh.png](http://sci2s.ugr.es/sites/default/files/files/ComplementaryMaterial/imbalanced/yeast4_s1.0tr_mcg_vs_gvh.png)

(<a href="#top">Back to top</a> \| [picture source](http://sci2s.ugr.es/sites/default/files/files/ComplementaryMaterial/imbalanced/yeast4_s1.0tr_mcg_vs_gvh.png))
<hr>

### How to combat classification imbalance?

1. Can You Collect More Data?
	
	A larger dataset might expose a different and perhaps more balanced perspective on the classes
	
2. Try Changing Your Performance Metric

	* Confusion Matrix: A breakdown of predictions into a table showing correct predictions (the diagonal) and the types of incorrect predictions made (what classes incorrect predictions were assigned).
	* Precision: A measure of a classifiers exactness.
	* Recall: A measure of a classifiers completeness
	* F1 Score (or F-score): A weighted average of precision and recall.

3. Try Resampling Your Dataset

	* Consider testing under-sampling when you have an a lot data (tens- or hundreds of thousands of instances or more)
	* Consider testing over-sampling when you don’t have a lot of data (tens of thousands of records or less)
	* Consider testing random and non-random (e.g. stratified) sampling schemes.
	* Consider testing different resampled ratios (e.g. you don’t have to target a 1:1 ratio in a binary classification problem, try other ratios)

4. Try Generate Synthetic Samples
5. Try Different Algorithms

	That being said, decision trees often perform well on imbalanced datasets. The splitting rules that look at the class variable used in the creation of the trees, can force both classes to be addressed.

6. Try Penalized Models

	Penalized classification imposes an additional cost on the model for making classification mistakes on the minority class during training. These penalties can bias the model to pay more attention to the minority class.


7. Try a Different Perspective

	There are fields of study dedicated to imbalanced datasets. They have their own algorithms, measures and terminology.
	Two you might like to consider are anomaly detection and change detection.


(<a href="#top">Back to top</a> \| [source](http://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/))
<hr>




### What is the apriori principle?
"A priori means “from before” in Latin. When defining a problem, it’s common to state prior knowledge, or assumptions. This is written as “a priori.” In Bayesian statistics, it’s common to make inferences conditional upon this a priori knowledge. A priori knowledge can come from domain knowledge, previous measurements, and so on."


(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))
<hr>

### What is a general approach to the Apriori algorithm?

General approach to the Apriori algorithm1. Collect: Any method.2. Prepare: Any data type will work as we’re storing sets.3. Analyze: Any method.4. Train: Use the Apriori algorithm to find frequent itemsets.5. Test: Doesn’t apply.6. Use: This will be used to find frequent itemsets and association rules between items.


(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<hr>


### What is a general approach to FP-growth?

General approach to FP-growth1. Collect: Any method.2. Prepare: Discrete data is needed because we’re storing sets. If you have contin- uous data, it will need to be quantized into discrete values.3. Analyze: Any method.4. Train: Build an FP-tree and mine the tree.5. Test: Doesn’t apply.6. Use: This can be used to identify commonly occurring items that can be used to make decisions, suggest items, make forecasts, and so on.

(<a href="#top">Back to top</a> \| [source](([source](https://www.manning.com/books/machine-learning-in-action))))

<a href="#top">Back to top</a>
<hr>

### What is a ROC curve? And what is a learning curve?

ROC (Receiver operating characteristic) curve and learning curve are synonymous

"A ROC curve is a graphical depiction of classifier performance that shows the trade-off between increasing true positive rates (on the vertical axis) and increasing false positive rates (on the horizontal axis) as the discrimination threshold of the classifier is varied. Thus, only a single parameter (the decision / discrimination threshold) associated with the model is changing at different points on the plot. This ROC curve (from Wikipedia) shows performance of three different classifiers."




### What is a generative model?

In probability and statistics, a Generative Model is a model used to generate data values when some parameters are hidden. Generative models are used in Machine Learning for either modeling data directly or as an intermediate step to forming a conditional probability density function. In other terms you model p(x,y) in order to make predictions (which can be converted to p(x|y) by applying the Bayes rule) as well as to be able to generate likely (x,y) pairs, which is widely used in Unsupervised Learning. Examples of Generative Models include Naive Bayes, Latent Dirichlet Allocation and Gaussian Mixture Model.


(<a href="#top">Back to top</a> \| 
[source](http://www.datasciencecentral.com/m/blogpost?id=6448529:BlogPost:305211&utm_content=buffer7008f&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer))

<hr>


### What is a discriminative model?
Discriminative Models or conditional models, are a class of models used in Machine Learning to model the dependence of a variable y on a variable x. As these models try to calculate conditional probabilities, i.e. p(y|x) they are often used in Supervised Learning. Examples include Logistic Regression, SVMs and Neural Networks.


(<a href="#top">Back to top</a> \| 
[source](http://www.datasciencecentral.com/m/blogpost?id=6448529:BlogPost:305211&utm_content=buffer7008f&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer))

<hr>


### What is uplift modelling?

Uplift modelling uses a randomised scientific control to not only measure the effectiveness of a marketing action but also to build a predictive model that predicts the incremental response to the marketing action. It is a data mining technique that has been applied predominantly in the financial services, telecommunications and retail direct marketing industries to up-sell, cross-sell, churn and retention activities.

![http://api.ning.com/files/7KfVtj4CX6gk*fzvtENrs09SPPYcEF7I*0Jg2oENWu1zQh0FQck5dctviIh-WkJrkhsaPlWt1MWAHc36gCmC4iDskfS*boyB/upliftcustomers.jpg](http://api.ning.com/files/7KfVtj4CX6gk*fzvtENrs09SPPYcEF7I*0Jg2oENWu1zQh0FQck5dctviIh-WkJrkhsaPlWt1MWAHc36gCmC4iDskfS*boyB/upliftcustomers.jpg)

[picture source](http://api.ning.com/files/7KfVtj4CX6gk*fzvtENrs09SPPYcEF7I*0Jg2oENWu1zQh0FQck5dctviIh-WkJrkhsaPlWt1MWAHc36gCmC4iDskfS*boyB/upliftcustomers.jpg)


### What are examples of transformations used in data analysis?


![https://statswithcats.files.wordpress.com/2010/11/table-of-transformations-2.jpg](https://statswithcats.files.wordpress.com/2010/11/table-of-transformations-2.jpg)

(<a href="#top">Back to top</a> \| [source]())

<hr>


![http://i.stack.imgur.com/yM4xY.png](http://i.stack.imgur.com/yM4xY.png)

([picture source](http://i.stack.imgur.com/yM4xY.png))

(<a href="#top">Back to top</a> \| [source](http://stackoverflow.com/questions/4617365/what-is-a-learning-curve-in-machine-learning))

<hr>



### What is the multi-class logarithmic loss?

Logarithmic loss is a metric commonly used to grade predictions on [kaggle](www.kaggle.com).

This is the multi-class version of the Logarithmic Loss metric. Each observation is in one class and for each observation, you submit a predicted probability for each class. The metric is negative the log likelihood of the model that says each test observation is chosen independently from a distribution that places the submitted probability mass on the corresponding class, for each observation.

logloss=−1/N * ∑i=1N * ∑j=1M y_i,j log(p_i,j)

where N is the number of observations, M is the number of class labels, loglog is the natural logarithm, yi,jyi,j is 1 if observation ii is in class jj and 0 otherwise, and pi,jpi,j is the predicted probability that observation ii is in class jj.

Both the solution file and the submission file are CSV's where each row corresponds to one observation, and each column corresponds to a class. The solution has 1's and 0's (exactly one "1" in each row), while the submission consists of predicted probabilities.

The submitted probabilities need not sum to 1, because they will be rescaled (each is divided by the sum) so that they do before evaluation.

(Note: the actual submitted predicted probabilities are replaced with max(min(p,1−10−15),10−15)max(min(p,1−10−15),10−15).)
{% highlight python linenos %}
id,col1,col2,Indicator
1,1,0,Public
2,1,0,Public
3,1,0,Public
4,0,1,Public
5,0,1,Public
6,0,1,Public
7,1,0,Private

id,col1,col2
1,0.5,0.5
2,0.1,0.9
3,0.01,0.99
4,0.9,0.1
5,0.75,0.25
6,0.001,0.999
7,1,0
{% endhighlight %}


(<a href="#top">Back to top</a> \| [source](https://www.kaggle.com/wiki/MultiClassLogLoss))

<hr>


## Neural networks


### What is the sigmoid function?

A sigmoid function is a mathematical function having an "S" shape (sigmoid curve)

It is used in neural networks to give logistic neurons real-valued output that is a smooth and bounded function of their total input. 

It also has the added benefit of having nice derivatives which make learning the weights of a neural network easier. 

([source](https://en.wikipedia.org/wiki/Sigmoid_function))

![https://upload.wikimedia.org/wikipedia/commons/f/f1/Sigmoid-function.svg](https://upload.wikimedia.org/wikipedia/commons/f/f1/Sigmoid-function.svg)

(<a href="#top">Back to top</a> \| [picture source](https://upload.wikimedia.org/wikipedia/commons/f/f1/Sigmoid-function.svg))

<hr>



## DeepLearning

### What is a perceptron?

A perceptron is a type of artificial neuron (another type is e.g. sigmoid neuron).
The perceptron can take a series of inputs and outputs a single binary output. The different inputs can be weighted to express the importance of the respective inputs to the output.
The neurons output, 0 or 1, is determined by whether the sum of all products (weights * input) exceeds a defined threshold.

([source](http://neuralnetworksanddeeplearning.com/chap1.html))

![http://www.amax.com/blog/wp-content/uploads/2015/12/blog_deeplearning1.jpg](http://www.amax.com/blog/wp-content/uploads/2015/12/blog_deeplearning1.jpg)

(<a href="#top">Back to top</a> \| [picture source](http://www.amax.com/blog/wp-content/uploads/2015/12/blog_deeplearning1.jpg))


<hr>


### How can you use a perceptron to model a simple logical function (e.g. a NAND gate)?

Given the following perceptron:

![http://lauraskelton.github.io/images/posts/4neuralnet_perceptron.png](http://lauraskelton.github.io/images/posts/4neuralnet_perceptron.png)

([picture source](http://lauraskelton.github.io/images/posts/4neuralnet_perceptron.png))

It generates the following outputs:

* the input 00 produces (−2)\*0+(−2)\*0+3=3 => 1
* the input 01 and 10 produces 1
* and input 11 produces (−2)\*1+(−2)\*1+3=-1 => 0.

Which show that this perceptron indeed models a NAND gate.

([source](http://neuralnetworksanddeeplearning.com/chap1.html))

<a href="#top">Back to top</a>
<hr>


### Put deep learning into perspective to other learning algorithms.


![https://www.safaribooksonline.com/library/view/practical-machine-learning/9781784399689/graphics/B03980_11_63.jpg](https://www.safaribooksonline.com/library/view/practical-machine-learning/9781784399689/graphics/B03980_11_63.jpg)

([picture source](https://www.safaribooksonline.com/library/view/practical-machine-learning/9781784399689/graphics/B03980_11_63.jpg))

<a href="#top">Back to top</a>
<hr>



### How does backpropagation work?
The probably best resource to learn how backpropagation works is to look at this step-by-step example [here](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/).

Backpropagation is usually succeeded by a 1. forward pass to get an initial prediction of the model.
The goal of backpropagation is to update weights so that actual and predicted value are close (minimizing squared root error).

![https://i.ytimg.com/vi/An5z8lR8asY/maxresdefault.jpg](https://i.ytimg.com/vi/An5z8lR8asY/maxresdefault.jpg)

([picture source](https://i.ytimg.com/vi/An5z8lR8asY/maxresdefault.jpg))


<a href="#top">Back to top</a>
<hr>




### How could a trainig workflow for deep learning look like?
We train the model on our training set for an epoch at a time. At the end of each epoch, we ensure that our error on the training set and validation set is decreasing. When one of these stops to improve, we terminate and make sure we’re happy with the model’s performance on the test data. If we’re unsatisfied, we need to rethink our architecture. If our training set error stopped improving, we probably need to do a better job of capturing the important features in our data. If our validation set error stopped improving, we probably need to take measures to prevent overfitting. 

 

If, however, we are happy with the performance of our model on the training data, then we can measure its performance on the test data, which the model has never seen before this point. If it is unsatisfactory, that means that we need more data in our dataset because the test set seems to consist of example types that weren’t well represented in the training set. Otherwise, we are finished!

[source](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/ch02.html)

![https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/deep_learning_workflow.png](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/deep_learning_workflow.png)

([picture source](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/deep_learning_workflow.png))

<a href="#top">Back to top</a>
<hr>


### What is the softmax function?

The softmax function is important in the field of machine learning because it can map a vector to a probability of a given output in binary classification.

The softmax (logistic) function is defined as:

![https://qph.ec.quoracdn.net/main-qimg-15dba2e5270a77afdfd2c86dc4757a17?convert_to_webp=true](https://qph.ec.quoracdn.net/main-qimg-15dba2e5270a77afdfd2c86dc4757a17?convert_to_webp=true)

where θ represents a vector of weights, and x is a vector of input values. This function is used to approximate a target function y∈{0,1} in binary classification. The softmax function produces a scalar output hθ(x)∈R,0<hθ(x)<1.

![https://qph.ec.quoracdn.net/main-qimg-cc09d4e526c39dddfe957b280a2e4f0c?convert_to_webp=true](https://qph.ec.quoracdn.net/main-qimg-cc09d4e526c39dddfe957b280a2e4f0c?convert_to_webp=true)

This can be seen as the confidence that your test point has an output value of 1. When −θTx  is very small, then the probability y=1  is small. When −θTx  is very large, hθ(x) approaches 1 as the probability that y=1  approaches 100%.

Note that this is also widely used in artificial neural network design, as the "activation function" of each neuron. Each neuron receives a vector of outputs from other neurons that fired, each axon with its own weighting. These are then linearly combined and used in the softmax function to determine if the next neuron fires or not.

[source](https://www.quora.com/How-does-softmax-function-work-in-AI-field)

<a href="#top">Back to top</a>
<hr>

### What is dropout and what is it used for?
Dropout is a form of regularisation.

How does it work?
It essentially forces an artificial neural network to learn multiple independent representations of the same data by alternately randomly disabling neurons in the learning phase.

What is the effect of this?
The effect of this is that neurons are prevented from co-adapting too much which makes overfitting less likely.

![http://engineering.flipboard.com/assets/convnets/dropout.png](http://engineering.flipboard.com/assets/convnets/dropout.png)

Why does this happen?
The reason that this works is comparable to why using the mean outputs of many separately trained neural networks to reduces overfitting.

[source](https://www.quora.com/How-does-the-dropout-method-work-in-deep-learning)

<a href="#top">Back to top</a>
<hr>


## Advanced questions

