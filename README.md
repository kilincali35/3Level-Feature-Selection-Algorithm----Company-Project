# 3 Level feature selection Algorithm for huge datasets


In our work environment, we have been dealing with datasets having up to 500 features. This increases the noise and handling time for a single algorithm. Selecting top 20-30 features among these 500 with high accuracy, is very important concept in our work in Afiniti. Our main models need to be precise and need to have good performance on production. Feeding the model with important features rather than noisy ones, is crucial part of our model development process. 

That is why i created a multi level feature selection algorithm for having more correct importance scores for these variables. In the upper 2 level, there is a part where Recursive Feature Selection algorithm uses Permutation Feature Selection(on Decision Tree). This part decreases the feature pool into 100 features, selecting the top 100 ones among all of the features.

After that, these 100 features are fed into a CatBoost algorithm, Classifier or Regressor according to the target variable. And CatBoost algorithm gives us Feature Importance scores at the end. We mostly choose top 30 of these features to use in our models mainly. 

Of course there are many preprocessing steps before running these 3 levels. Imbalance checks are done, if needed target is balanced. High cardinality features are detected and eliminated if necessary. Fix, empty, duplicate, or highly null columns are detected; and eliminated.

For multicollinearity, this sub algorithm is working. Create a correlation matrix among all numerical variables. Find the highest one which is over threshold. Calculate average correlation of each variable in this pair with other independent variables. Eliminate the higher correlated one. Then go to the beginning step, re create the correlation matrix. Repeat this process until no correlation pair over threshold is left.


