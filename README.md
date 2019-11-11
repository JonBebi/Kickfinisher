# Kickfinisher

This project is about trying to predict the success of a Kickstarter project before it launches.

### Source:
https://www.kaggle.com/kemical/kickstarter-projects
There are more than 300,000 Kickstarter projects from 22 countries.

## EDA

I dropped the rows with Nan values. The loss in data points wasn't relevant according to me.
I decided to choose US data for training, the largest source. The target variable is the state of the project.
Originally in the dataset there are 5 states:
* Successful
* Canceled
* Failed
* Suspended
* Live

Live projects were dropped and I reclassified the canceled, failed and suspended as unsuccessful. I have to investigate in the future if instead I should have kept just the projects with a successful and failed state.

After my classification there are:
* __109,299__ _successful (1)_
* __181,585__ _unssuccesful (0)_
![StateDistribution](https://github.com/JonBebi/Kickfinisher/blob/master/Visualizations/StateDistribution.png "State distribution")

As I am trying to predict success before launch I was limited on the features:
* __Main category__ (15)
* __Goal__ (amount of USD trying to reach)
* __Launched__ (only the month when the project launches)
* __Time__ (amount of days available to reach the goal)

The main categories diverge into other categories, but it would have been to many of them, approximately 10 times more, so I decided to use the main ones.
I decided to extract just the month when the project launches as it might make a difference what time of the year the project is out there.

_The distribution of the __projects__ based on the __months__(1-12) they launched_
![DistributionMonthLaunched](https://github.com/JonBebi/Kickfinisher/blob/master/Visualizations/DistributionMonthLaunched.png "The distribution of the months the projects were launched")

___Feature importance__ based on the __Random Forest__ model_
![FeatureImportance](https://github.com/JonBebi/Kickfinisher/blob/master/Visualizations/FeatureImportance.png "Feature importance based on the Random Forest model")

## Modeling

To account for the class imbalance I considered trying SMOTE and NearMiss and actually applied SMOTE as gave slightly better results.

### Accuracy scores of models ran on US

* __Dummy Classifier__: _62.26%_
* __KNN__ (best k tuning): _61.5%_
* __Decision Tree__ (manual tuning): _64.55%_
* __Random Forest__ (manual tuning): _65.27%_
* __XGBoost__: _65.33%_
* __XGBoost__ (GridSearchCV tuning): _65.33%_

### Accuracy scores of models ran on other countries

__GB__
* __Decision Tree__: _64.81%_
* __Random Forest__: _65.4%_
* __XGBoost__: _66.7%_

__CA__
* __Decision Tree__: _67.43%_
* __Random Forest__: _68.02%_
* __XGBoost__: _69.29%_

### _Slide presentation_:
https://docs.google.com/presentation/d/1Kvj8NlkpkhXqdh9uAscw7O8LpFq-81ChXF-F7HXyPnU/edit?usp=sharing
