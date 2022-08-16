# _CST 383 - Team Project: Life Expectancy_

---

## **Authors**: Larry Chiem, Ian Rowe, Raymond Shum, Nicholas Stankovich

---

## **Video**: [Watch it on YouTube!](https://youtu.be/pR06KVtDhz4)

---

## **Table of Contents:**
1. [Introduction](#introduction)
1. [Selection of Data](#selection-of-data)
1. [Methods](#methods)
1. [Results](#results)
1. [Discussion](#discussion)
1. [Summary](#summary)
1. [References](#references)
---
---

## Introduction
---
The purpose of our experiment was to identify the predictors and model that would provide the most accurate predictions of our target variable, life expectancy. We used linear regression as our supervised machine learning algorithm of choice and test RMSE as our measure of accuracy. As we progressed through our experiments, we attempted to further lower test RMSE through the use of forward feature selection and unsupervised learning using polynomial features. 

## Selection of Data
---

We used the following publicly available Kaggle data set: [Life Expectancy (WHO)](https://www.kaggle.com/kumarajarshi/life-expectancy-who)

This dataset contains 22 features, including our target variable: 'life expectancy', with up to 2938 entries per feature.

Initial inspection revealed that the data set had several issues including missing data and possibly bad data in the form of extreme outliers. We began by dropping features that we determined the be unnecessary and imputing missing values. Through data exploration, we identified potential features that could be dropped (highly correlated features in the subset of predictors) and potential features that could be included (predictors highly correlated with our target variable).

In terms of feature engineering, we performed log transforms of the following predictors: percentage expenditure, gdp, hiv/aids and bmi. We replaced the original predictors with these feature engineered predictors in our third experiment. We did so after confirming that these transformed features were more correlated with the target variable than the original ones.

## Methods
---

We used the following materials, APIs and tools (including Python libraries):
- Jupyter Notebook and Anaconda
- Pandas
- Numpy
- Matplotlib
- SciPy
- scikit-learn
- Kaggle

Following the actions outlined in the previous section, Selection of Data, our experiment was executed in the following phases.

In the first phase, we ran three experiments. The first experiment fit a linear regression model to a feature set containing all available predictors. This was done to establish a baseline test RMSE against which we could compare results from feature selection, feature engineering and tuning of our model. In our second experiment, we selectively included and excluded features in our model based on the results of our previous data exploration. In the third experiment, we developed another model in which we replaced some columns with feature engineered (log transformed) ones. 

In the second phase, we attempted to see if we could improve the accuracy of our feature engineered data set by tuning our model through the use of Forward Feature Selection. 

In the third phase, we attempted to improve the accuracy of our previously developed models by accounting for possible interaction between features. We applied polynomial features to our 4 previously developed models (experiments 1-3 in phase 1 and experiment 4 in phase 2).

## Results
---
For reference, here are the initial properties of our dataset, determined before testing:
- 'blind' RMSE: 9.7
- Standard Deviation of life expectancy: 9.5

The 'blind' RMSE was calculated by using the mean value of RMSE as the predicted value (taking the root of the square of differences between the mean and test values).

In our first phase, we observed the following results:
- Experiment 1 (baseline) - Test RMSE: 4.0, Training R-Squared: 0.83
- Experiment 2 (select features) - Test RMSE: 4.5, Training R-Squared: 0.78
- Experiment 3 (feature engineering) - Test RMSE: 4.1, Training R-Squared: 0.82

In our second phase, we observed the following results:
- Experiment 4 (forward feature selection of engineered data set) - Lowest Test RMSE: 3.63

In our third phase, we fit polynomial features to our previous experiments and observed the following results:
- Experiment 5 (refit Exp. 4) - Test RMSE: 1.82, Training R-Squared: 0.98
- Experiment 6 (refit Exp. 1) - Test RMSE: 3.79, Training R-Squared: 0.88
- Experiment 7 (refit Exp. 2) - Test RMSE: 3.04, Training R-Squared: 0.91
- Experiment 8 (refit Exp. 3) - Test RMSE: 3.52, Training R-Squared: 0.87

## Discussion
---
We believe that our experiments addressed two issues relevant to the linear regression model. 

First, as mentioned in lecture, linear regression assumes a linear relationship between the target variable and predictors. In a relationship where the data is 'curved', feature engineering can be used to improve the linear fit. This is most apparent in experiment 3, where including log transforms of select predictors produced the lowest test RMSE in our first phase of testing.

Second, also mentioned in lecture, predictors cannot interact in a plain linear model. We believe that our results demonstrate the importance of capturing possible interactions between predictors. In the first phase of testing (using manual feature selection and engineering), none of our experiments performed better than the baseline. However, after fitting polynomial features to the set of our predictors (accounting for interactions), all experiments performed better than the baseline.

However, it is worth noting that it was not impossible to beat the baseline score without fitting polynomial features. We also note that greedy algorithms are effective in selecting predictors in circumstances where the team is unable to do so effectively due to the nature of the data or (in our case) inexperience. Using forward feature selection, we were able to beat the baseline test RMSE after four features were selected. Our best experiment resulted in using forward feature selection to pick the most impactful predictors and then account for interactions through the inclusion of polynomial features. 

We would also like to note a few caveats to our results:

First, we performed the experiment sub-optimally. Ideally, we would first use a validation curve to identify the best polynomial degree we could use for our polynomial features. After fitting polynomial features, we would use forward feature prediction to select the most impactful predictors. This way, the algorithm would also be able to select from the pool available interaction features. Afterwards, we could use a learning curve to identify either a high bias or high variance situation and further tune the model from there. While we were unable to execute this strategy due to time constraints, it is a potential area for further research. 

Second, our best model (experiment) has an extremely high training rsquared value at 0.98. This implies an overfit situation (where it might just be memorizing the training data). However, it also produced the lowest test RMSE at 1.82. If we had more data available for testing and training, the results may not hold up. We have some ideas on why this might be happening. For example, did our method of imputation (KNN) and parameters lead to predictors that were more highly correlated with each other? We were unable to investigate this issue due to time constraints, but it represents another area for future research.

## Summary
---

For this project, our group performed a series of experiments in order to find the best predictors and linear regression model for the prediction of life expectancy. We found that feature engineering and inclusion of feature interactions are important in overcoming the inherent assumptions of a linear regression model through the inclusion of polynomial features. Starting with a baseline test RMSE score of 4.0 (while the target variable had an STD of 9.5), we were able to improve our model to produce a test RMSE of 1.82 and identify the most impactful predictors (included in the notebook). While we believe that we have met our original goals, based on the results, we also believe there is much room for improvement. We have identified areas of further research that we were unable to address within this project, such as improvements to our data preprocessing and model tuning stages. 

## References

---

Géron Aurélien. (2019). _Hands-on machine learning with scikit-learn, Keras, and tensorflow: Concepts, tools, and techniques to build Intelligent Systems_. O&#39;Reilly Media, Inc.

VanderPlas, J. T. (2017). _Python Data Science Handbook: Essential Tools for working with data_. O&#39;Reilly Media, Inc.

---

[Return to Top](#table-of-contents)
