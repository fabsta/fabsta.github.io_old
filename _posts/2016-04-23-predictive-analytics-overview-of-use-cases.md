---
title: "Predictive analytics: overview of use cases"
description: "Predictive analytics: overview of use cases"
category: datascience
tags: [datascience]
sidebar:
  nav: "new_side"
---

### Table of contents

* TOC
{:toc}



# Use cases

## Understanding markets

### Preference of mobile communication services

<img src="{{base}}/images/datascience/usecase_preference_marketing.jpg" width="600px"><br>
Spine Chart of Preferences for Mobile Communication Services ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/01fig01.jpg))

(<a href="#top">Back to top</a>)
<hr>

### Marketplace behaviour
A framework for understanding marketplace behavior—the choices of buyers and sellers in a market.<br>
<img src="{{base}}/images/datascience/use_case_markets_sellers_buyers.jpg" width="600px"> ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/01fig02.jpg))

## Predicting customer choice: Transportation study - predicting train or car

### Example input data
```python
cartime,carcost,traintime,traincost,choice
70,50,64,39,TRAIN
50,230,60,32,TRAIN
50,70,58,40,CAR
60,108,93,62,CAR
70,60,68,26,TRAIN
```

### Visually explore variables

<img src="{{base}}/images/datascience/use_case_transportation_explore.jpg" width="300px"><br>
Scatter Plot Matrix for Explanatory Variables in the Sydney Transportation Study ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/02fig01.jpg))

#### What are the correlations between the different features?
<img src="{{base}}/images/datascience/use_case_transportation_correlation.jpg" width="300px"><br>
Correlation Heat Map for Explanatory Variables in the Sydney Transportation Study ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/02fig01.jpg))

(<a href="#top">Back to top</a>)
<hr>

### Build regression model and look at it

A linear combination of the four explanatory variables is used to predict consumer choice. The resulting logistic regression model is:

<img src="{{base}}/images/datascience/use_case_transportation_regression_model.jpg" width="400px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/02tab01.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Predicting probability to take the train/car

<img src="{{base}}/images/datascience/use_case_transportation_predict_car_train.jpg" width="300px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/02fig03.jpg)

(<a href="#top">Back to top</a>)
<hr>

### How much lower do ticket prices need to be so that more people take the train?
Goal: Increase public transportation usage by 10 percent. 

<img src="{{base}}/images/datascience/use_case_transportation_how_lower_price.jpg" width="300px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/02fig04.jpg)

Conclusion:
183 (55 percent) of commuters would take the train if ticket prices were lowered by 5 cents

(<a href="#top">Back to top</a>)
<hr>

## Targeting current customers: Target marketing (Bank marketing study)

### Exploration

#### Age of client vs response to marketing
<img src="{{base}}/images/datascience/use_case_target_marketing_age.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig01.jpg)


(<a href="#top">Back to top</a>)
<hr>

#### Education level vs response to marketing

<img src="{{base}}/images/datascience/use_case_target_marketing_education.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig02.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Job type vs response to marketing

<img src="{{base}}/images/datascience/use_case_target_marketing_job.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig03.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Martial status vs response to marketing
<img src="{{base}}/images/datascience/use_case_target_marketing_martial.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig04.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Has housing loans vs response to marketing
<img src="{{base}}/images/datascience/use_case_target_marketing_housing.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig04.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Logistic regression

#### Density lattice
Logistic Regression for Target Marketing (Density Lattice)<br>

<img src="{{base}}/images/datascience/use_case_target_marketing_log_regression.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig06.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Confusion matrix
Logistic Regression for Target Marketing (Confusion Mosaic)<br>

<img src="{{base}}/images/datascience/use_case_target_marketing_confusion_matrix.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig07.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Lift chart
Lift Chart for Targeting with Logistic Regression<br>

<img src="{{base}}/images/datascience/use_case_target_marketing_lift_chart.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig08.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Financial analysis of target marketing

<img src="{{base}}/images/datascience/use_case_target_marketing_financial_analysis.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/03fig09.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Finding new customers: Market segmentation (bank customers)

### Age across the five resulting market segments

<img src="{{base}}/images/datascience/use_case_markets_age_across.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/04fig01.jpg)


### Response to offer across segments

<img src="{{base}}/images/datascience/use_case_markets_response.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/04fig02.jpg)

### Describing market segments

<img src="{{base}}/images/datascience/use_case_market_responce_across_describing_markets.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/04fig03.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Retaining customers: How likely are customer to switch (Customer churn)?


### Telephone usage by service provider choice
Telephone Usage and Service Provider Choice (Density Lattice)<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_usage.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig01.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Probability to switch based on telephone usage
Telephone Usage and the Probability of Switching (Probability Smooth)<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_prop_to_switch.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig02.jpg)

(<a href="#top">Back to top</a>)
<hr>

### AT&T reach out plan and service provider choice

<img src="{{base}}/images/datascience/use_case_customer_churn_service_prod_choice.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig03.jpg)

(<a href="#top">Back to top</a>)
<hr>

### AT&T calling card and service provider choice

<img src="{{base}}/images/datascience/use_case_customer_churn_calling_cards.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig04.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Results of fitting a regression model
Logistic Regression Model for the AT&T Choice Study<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_fitting_regression.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05tab01.jpg)


Logistic Regression Model Analysis of Deviance<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_fitting_regression_deviance.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05tab02.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Predicted probability of switching 
Logistic Regression for the Probability of Switching (Density Lattice)<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_pred_switching.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig05.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Confusion mosaic
Logistic Regression for the Probability of Switching (Confusion Mosaic)<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_confusion_mosaic.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig06.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Reporting results as classification tree
A Classification Tree for Predicting Consumer Choices about Service Providers<br>

<img src="{{base}}/images/datascience/use_case_customer_churn_classification_tree.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/05fig07.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Positioning products: Movie example

## Developing new products

<img src="{{base}}/images/datascience/use_case_new_product.jpg" width="600px"><br>
The Precarious Nature of New Product Development ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/07fig01.jpg)).


## Promoting products: Evaluating the effect of promotions
Goal is to check if promotions during LA dodgers games have effect on attendance.

### Exploration

#### Dodgers Attendance by Day of Week

<img src="{{base}}/images/datascience/use_case_promotion_dodgers_attendance.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/08fig01.jpg)

(<a href="#top">Back to top</a>)
<hr>
#### Dodgers Attendance by Month

<img src="{{base}}/images/datascience/use_case_promotion_dodgers_attendance_month.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/08fig02.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Dodgers Weather, Fireworks, and Attendance

<img src="{{base}}/images/datascience/use_case_promotion_dodgers_attendance_weather.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/08fig03.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Dodgers Attendance by Visiting Team

<img src="{{base}}/images/datascience/use_case_promotion_dodgers_attendance_visiting.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/08fig04.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Regression model performance

<img src="{{base}}/images/datascience/use_case_promotion_regression_model.jpg" width="600px"><br>
[image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/08fig05.jpg)

(<a href="#top">Back to top</a>)
<hr>


## Recommending products: Shopping

<img src="{{base}}/images/datascience/use_case_shopping_list.jpg" width="600px"><br>
Market Basket for One Shopping Trip ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09tab01.jpg)).


<img src="{{base}}/images/datascience/use_case_basket_prevalence.jpg" width="600px"><br>
Market Basket Prevalence of Initial Grocery Items ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09fig01.jpg)).

<img src="{{base}}/images/datascience/use_case_basket_prevalence_category.jpg" width="600px"><br>
Market Basket Prevalence of Grocery Items by Category ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09fig02.jpg)).


<img src="{{base}}/images/datascience/use_case_basket_association.jpg" width="600px"><br>
Market Basket Association Rules: Scatter Plot ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09fig03.jpg)).


<img src="{{base}}/images/datascience/use_case_basket_association_matrix.jpg" width="600px"><br>
Market Basket Association Rules: Matrix Bubble Chart ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09fig04.jpg)).


<img src="{{base}}/images/datascience/use_case_basket_association_local_farmer.jpg" width="600px"><br>
Association Rules for a Local Farmer ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09fig05.jpg)).


<img src="{{base}}/images/datascience/use_case_basket_association_local_farmer_network.jpg" width="600px"><br>
Association Rules for a Local Farmer: A Network Diagram ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/09fig06.jpg)).


## Predicting Sales

### Example input data

```python
sales,competition,population,income
107919,3,65044,13240
118866,5,101376,22554
98579,7,124989,16916
122015,2,55249,20967
```

The features mean:

* Sales by store
* Potential competitors
* Population in that area
* Median income of houses <5 minutes of store away.


### Explore the variables

#### Pairwise relationship btw variables
<img src="{{base}}/images/datascience/13fig01.jpg" width="300px"><br>
Scatter Plot Matrix for Restaurant Sales and Explanatory Variables ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/13fig01.jpg)).

#### Correlation heat map
<img src="{{base}}/images/datascience/13fig02.jpg" width="300px"><br>
Correlation Heat Map for Restaurant Sales and Explanatory Variables ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/13fig02.jpg)).

### Linear regression

<img src="{{base}}/images/datascience/13fig03.jpg" width="300px"><br>
Fitted Regression Model for Restaurant Sales ([image source](https://www.safaribooksonline.com/library/view/marketing-data-science/9780133887662/graphics/13tab01.jpg)).


