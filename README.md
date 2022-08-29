# Project-3

## 1. Overview
The purpose of this notebook is to explore a data set of churned customers, and then build a predictive 
model that will indicated which customers are likely to churn.

Link to Technical Notebook: https://github.com/Kmulla19/Project-3
Link to Original Data Source: https://www.kaggle.com/datasets/becksddf/churn-in-telecoms-dataset

## 2. Business Understanding
SyriaTel wants to better understand what features are indicators that a customer is more likely to churn. Keeping an existing customer is cheaper than acuiring a new one so they want to be able to proactively reach out to customers and offer them incentives to stay.

## 3. Data Exploration
There were no nulls that needed to be dropped, but there are object columns to deal with. Decided to drop phone number becuase it does not seem relevant.

I explored a number of features to see how they are related to churn.

* Minutes Usage and Spend
* Account Features such as Voicemail and having an Internation Plan
* Use of Customer Service
* Location
* Account Length
* And More

I also created a new deep copy df to look more at minutes and spend. I created a deep copy becuase I didn't want these new features(columns) to later affect our model scoring.

These are the columns I created

* Total Minutes
* Total Charge
* Charge per Minute

Here are some of the top findings about customers who churn:

* Make 50% more customer service calls

* Don't use voicemail feature as much

* Spend almost 20% more on day charges

* Spend more in every category

* No difference in average acount length


Further individual exploration of these features revealed the following:

#### Spend and Minutes Used

Customers who churn spend $7 more a month than those who do not.

#### Customer Service

There is a signifcant difference in churn rate between 3 and 4 calls.


#### Voicemail and International Plan

Customers who churn are 46% less likely to use voicemail but 4x more likely to have an Intl plan.

#### Location

Two of the three highest rate states are California and Texas which are very populous, and the two lowest are Alaska and Hawaii which are very remote.


# 4. Models

First I created our initial Train Test Split

#### Processing Pipes

Next I created two subpipes and a column tranformer that will allow us to apply StandardScalar to our numerical features and OneHotEncoder for our categorical features. Then we placed both of these inside a ColumnTransformer

#### Model Pipes

Then I made model pipes for each of our various models we will be trying out

* Dummy Model
* Logistic Regression
* K Nearest Neighbors
* Random Forest

#### Cross Val Class

CrossVal
The below class will allow us to apply our pipes and perform a cross validation on the training data. It will also help us get our results afterwards, along with a violin plot.

#### Dummy Model
86% Accuracy

#### Logistic Regression Model
86% Accuracy

#### KNN Model
88% Accuracy
91% Training Score

I decided to perform a GridSearch on the KNN model to see how tuning the various hyperparameters would affet the score.

Here are the parameters I used.

* ['knn__n_neighbors'] = [1, 3, 5, 7, 9]
* ['knn__leaf_size'] = [20, 30, 40]
* ['knn__metric'] = ['minkowski', 'manhattan']

The GridSearch did not improve performance.

#### Random Forest Model
93% Accuracy

I looked at the top features for the Random Forest model. They are:

* number of voicemail messages
* international plan
* total international minutes
* total day charege
* total day minutes


Our final model's accuracy on the test set is 0.94. 

Our final model's recall on the test set is 0.62 

Our final model's precision on the test set is 0.99 

Our final model's f1-score on the test is 0.76.


# 4. Recommendations

#### Conduct an onboarding survey

* Determine the account type
* Do they need voicemail?
* Intl plan?

#### Elevate Customer Service

* Flag account at 2 calls. Note mentions of cancellation and cost.
* Elevate support at 3 calls.

#### Incentives

* $58 a month from 1/3 of churned customers is $9,338
* Free Voicemail

#### Additional Opportunities

* Recontact closed lost customers
* Further expand in HI & AK

