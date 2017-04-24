# Ensemble

## Combining Multiple Models

  - Build different "experts"
  - Often improves predictive performance
  - Usually produces hard to interpret data

## Bagging

  - Combining predictions by averaging/voting
    - Simplest way
    - Each model equally weighted
  - Ideally
    - Sample several training sets of size n
    - Build classifier for each training set
    - Combine predictions
  - Combine same type of learning algorithms
  - When learning scheme is unstable, bagging improves performance most of the time

## Bias-Variance Decomposition

  - Total error of classifier is the sum of bias and variance
    - **Bias**
      - Measures how well it matches problem
      - Persistent error (can't be eliminated)
    - **Variance**
      - Overall possible training and test sets
  - Combining multiple classifiers decreases expected error rate by reducing the variance

## Bagging Classifier

  - Works because reduces variance by voting (for classifier) or averaging (numeric prediction)
  - **Problem:** Only have one dataset
  - **Solution:** Generate new datasets of size n by sampling it with replacement - bootstrap aggregating
  - Fails with stable learning algorithms

## Randomization

  - Randomize learning algorithm instead of input
    - Some algorithms have random component
    - Most algorithms can be randomized
      - e.g. attribute selection in decision tree
    - Generally more applicable than bagging
    - Combining with bagging is possible

## Boosting

  - Uses voting/averaging, combines same type of learning algorithms
  - Weights models according to performance
  - Iterative
  - Several variants
  - Requires weights
    - Adapts learning algorithm
    - Apply boosting without weights
      - Resample probability determined by weights
      - High weight instances are replicated more frequently
      - Not all instances are used
      - if error > 0.5, can resample
  - Stems from computational learning

## Stacking

  - Used to combine different learning algorithms
  - Uses meta-learning rather than voting to determine which classifiers are more reliable
  - Two levels of learning
    - **Base learners:** level-0 models
    - **Meta learners:** level-1 model
  - Can't use predictions on training data to generate level-1 model
  - Hard to analyze
