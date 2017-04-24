# Evaluation

  - Error on training data is not good indicator of performance on future data
  - Can be used if lots of (labelled) data is available
    - Split data into training and test sets
  - Labelled data is usually limited

## Training and Testing

  - Natural performance measure for classification problems: Error rate
    - **Success:** Predicted correctly
    - **Error:** Predicted incorrectly
    - **Error Rate:** Proportion of errors made over instances
  - **Re-substitution Error:** Error rate obtained from training data

  - **Test set:** Independent instances that have no part in formation of classifier
    - Assumes both training and testing are samples of problem
  - May need multiple sets of data: Training, testing, validation
    - Build from training set
    - Optimize from validation set
    - Test from testing set
  - Once evaluator is complete, all data is used to build classifier
  - **Holdout procedure:** Method of splitting the original data into testing and training sets

## Predicting Performance

  - Prediction is similar to tossing biased coin
  - In statistics, succession of independent events is _Bernoulli process_

## Confidence Intervals - ok skip this bc stats

## Holdout Estimation

  - _Holdout method_ reserves certain amount for testing and training
    - Usually one third for testing
  - **Problem:** Samples may not be representative
  - Advanced version uses _stratification_
    - Ensures each class is represented with equal proportions in both subsets

## Cross-validation

  - Avoids overlapping test sets
    - Split data into k subsets
    - Use each subset for testing, remainder for training
  - k-fold cross-validation
  - Subsets often stratified before cross-validation is performed
  - Error estimates are averaged to produce overall error estimate
  - **Standard:** Stratified ten-fold cross-validation
  - Repeated stratified cross-validation is better

## Leave-one-out Cross-Validation

  - Form of cross-validation
    - n training instances -> builds classifier n times
  - **Advantages**
    - Makes best use of the data
    - No random subsampling
  - **Disadvantages**
    - Computationally expensive
    - Stratification is impossible
  - Example: Random dataset split into two equal classes
    - Best inducer predicts majority class
    - 50% accuracy on fresh data
    - Leave-one-out CV estimate is 100% error

## Bootstrap

  - Cross validation uses sampling without replacement
    - Same instance, once selected, cannot be selected again for training or testing
  - Uses sampling with replacement to form training set
    - Sample a dataset of n instances n times with replacement to form a new dataset of n instances
    - Uses this dataset as training set
    - Uses instances from original dataset that don't occur in new training set for testing
  - 0.632 Bootstrap
    - Probability of 1-1/n of not being picked
    - Training data will contain approximately 63.2% of the instances
  - Best way of estimating performance on very small datasets
  - Some problems
    - Perfect memorizer will achieve 0% re-substitution error, but ~50% true error rate

## Estimating Error for the 0.632 Bootstrap

  - Error estimate is pessimistic
    - Trained on ~63% of instances
  - Combine with re-substitution error
    - _err = 0.632 * e<sub>test_instances</sub> + 0.368 * e<sub>training_instances</sub>_
  - Re-substitution error gets less weight than error on test data
  - Repeat process with different replacement samples; average results

## Comparing Data Mining Schemes

  - Show scheme A is better than scheme  B in particular domain
    - For given amount of training data
    - Across all possible training sets on average
  - Assuming infinite data from domain
    - Sample infinitely many datasets of specified size
    - Obtain CV estimate on each dataset for each scheme
    - Check mean accuracy for scheme A is better than B
  - In practice, limited data and limited number of estimates for computing mean

## Predicting Probabilities

  - Also called 0-1 lass function
    - 0 if prediction is correct
    - 1 if incorrect
  - Most classifiers produce class probabilities
  - Depending on application, may need to check accuracy of the probability estimates
    - Don't use 0-1 loss here lmao

## Quadratic Loss Function

  - _p<sub>1</sub> ... p<sub>k</sub>_ are probability estimates for an instance
  - c is the index of an instance's actual class
  - _a<sub>1</sub> ... a<sub>k</sub> = 0_, except for _a<sub>c</sub>_ which is 1
  - Quadratic loss is
    - some long ass formula here
  - Can show minimized when _p<sub>i</sub> = p<sub>i</sub>*_, the true probabilities

## Informational Loss Function

  - _-log(p<sub>c</sub>)_, where _c_ is index of instance's actual class
  - Number of bits required to communicate the actual class
  - _-p<sub>1</sub>*log<sub>2</sub>p<sub>1</sub> - ... -p<sub>k</sub>*log<sub>2</sub>p<sub>k</sub>_, where _p<sub>1</sub>* ... p<sub>k</sub>*_ are the true class probabilities
  - **Difficulty:** Zero-frequency problem

## Comparing Quadratic and Informational Loss Functions

  - Both encourage honesty
  - Quadratic loss takes into account all class probability estimates for an instance
  - Informational loss focuses only on probability estimate for the actual class
  - Quadratic loss is bounded, can never exceed 2
  - Informational loss can be infinite

## Counting the Cost

  - In practice, different types of classification errors often incur different costs

  - Confusion matrix for two-class problem

  | | |Predicted|Class|
  |-------|---|---|---|
  |||Yes|No|
  | **Actual** |Yes|True Positive|False Negative|
  | **Class** |No|False Positive|True Negative|

  - TP rate = _TP / (TP + FN)_
  - FP rate = _FP / (TP + FN)_
  - Overall success rate = _(TP + TN) / (TP + TN + FP + FN)_
  - Error rate = _1 - success rate_

## Kappa Statistic

  - Measures relative improvement over random predictor
    - _(D<sub>observed</sub> - D<sub>random</sub>) / (D<sub>perfect</sub> - D<sub>random</sub>)_
  - Related to overall accuracy (success rate) of matrix

## Lift Charts

  - In practice, costs are rarely known, decisions made by comparing possible scenarios
  - **Example:** Mailout to 1,000,000 households
    - 0.1% response rate (1000)
    - Defines subset of 100,000 -> 0.4 respond (400)
      - Lift factor (0.4/0.1) = _4_
    - Subset of 400,000, 0.2% respond
      - Lift factor of _2_
