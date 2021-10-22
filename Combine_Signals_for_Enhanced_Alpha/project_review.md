# Combine Signals for Enhanced Alpha

This is the project review I got for the project "Combine Signals for Enhanced Alpha" in the "AI for trading" nanodegree

## Meets Specifications

Congratulations on finishing this project successfully  ![:tada:](https://review.udacity.com/assets/images/emojis/tada.png ":tada:")  Check out the below review for more feedback.

## Features and Labels

- [x] Describe the relationship between the shifted labels.

	That's correct! The autocorrelation decreases when the number of the lags for the labels increases

	The reason to look into the autocorrelation between the lagged labels is that if there's autocorrelation then that means that labels are not independent of each other which violates the core assumption of many of the machine learning models. Check out the  _Lesson 20: Overlapping Labels_  
So it is better not to have any autocorrelation between the class label samples.

- [x] Correctly implement the  `train_valid_test_split`  function.

	Nice work in splitting the data on level 0 which is date index of the multi-index dataframe, making sure not split a day between multiple datasets. It should be contained within a single dataset.

	Check out this Udacity video to see why the splitting of the data is needed to be done;  
[https://www.youtube.com/watch?v=Lmxem7ud9yk&list=PLAwxTw4SYaPn_OWPFT9ulXLuQrImzHfOV&index=16](https://www.youtube.com/watch?v=Lmxem7ud9yk&list=PLAwxTw4SYaPn_OWPFT9ulXLuQrImzHfOV&index=16)

## Random Forests

- [x] Describe why dispersion_20d has the highest feature importance, when the first split is on the Momentum_1YR feature.

	Check out the below paragraph taken from  *Lesson 21 Feature Importance, Section 6 When Feature Importance is Inconsistent*

	*Intuitively, if features 0 and 1 form the AND operator, then it makes sense that they should be equally important in determining the output. The feature importance calculated in sklearn assigns a higher importance to feature 0 compared to feature 1. This is because the tree first splits on feature 1, and then when it splits on feature 0, the labels become cleanly split into respective leaf nodes.*

	In other words, what we observe is that features which are used to split further down the bottom of the tree are given higher importance, using the gini/entropy impurity as a measure.

- [x] Describe how the accuracy changes over time and what indicates the model is overfitting or underfitting.

	Here the model is over-fitting and also under-fitting. It is under-fitting because this is binary classification task but the model still gets at 0.5 level of accuracy. The model is over-fitting because the performance on the validation set goes down while the performance on the training set improves.  
Check out this  [https://forums.fast.ai/t/can-a-model-overfit-and-underfit-at-the-same-time/50603/4](https://forums.fast.ai/t/can-a-model-overfit-and-underfit-at-the-same-time/50603/4)

## Overlapping Samples

- [x] Correctly implement the  `non_overlapping_samples`  function.

- [x] Correctly implement the  `bagging_classifier`  function.

	Random forest uses bagging technique. Check out the difference between random forest classifier and bagging classifier  [https://stats.stackexchange.com/questions/264129/what-is-the-difference-between-bagging-and-random-forest-if-only-one-explanatory](https://stats.stackexchange.com/questions/264129/what-is-the-difference-between-bagging-and-random-forest-if-only-one-explanatory)

- [x] Correctly implement the  `calculate_oob_score`  function.

	The out-of-bag is the validation set which is randomly taken out of the training set during the bootstrapping process. The out-of-bag (OOB) error is the average error for each validation set calculated using predictions from the trees that do not contain validation set in their respective bootstrap sample. This allows the  `RandomForestClassifier`  to be fit and validated whilst being trained.

- [x] Correctly implement the  `non_overlapping_estimators`  function.

	Nice work in creating subsets of the overlapping data to fit into the classifiers using  `non_overlapping_samples`  function by building a list of non-overlapping subsets of the data with different starting index. And then use each one of them to feed a classifier instead of using the same data to feed all classifiers.
