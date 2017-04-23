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

## Bootstrap

## Loss Function

## Kappa Statistic

## Lift Charts
