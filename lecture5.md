# Linear Models

## Linear Regression

  - Must work naturally with numeric attributes
  - Standard technique for numeric prediction
    - Outputs linear combination of attributes
      - x = w0 + w1a1 + w2a2 + w3a3 + ... + wkak
    - Weights calculated from training data
    - Add constant attribute a0 = 1 (bias)
    - w weight vector, a attribute vector

## Least Square Errors

  - Choose k + 1 coefficients (weights) to minimize the squared error on the training data
  - Derive coefficients from standard matrix operations
  - Can be done if instances > attributes
  - Linear regression model (least squared error linear regression model)

## Linear Classification

  - Any regression technique can be used
    - **Training:** Perform a regression for each class, setting output to 1 for training instances that belong to class, and 0 otherwise
    - **Result:** Linear expression for each class
    - **Prediction:** Predict class corresponding to model with largest output value
  - Multi-response linear regression

## Maximum Likelihood

   - **Aim:** Maximize probability of training data with respect to parameters
   - Can use logarithms of probabilities and maximize log-likelihood model
     - ravioli ravioli give me the formuloi

## Multiple Classes

  - Can perform logistic regression independently for each class
  - **Problem:** Probability estimates won't sum up to 1
  - **Better:** Train coupled models by maximizing likelihood over all classes
  - Alternatively - _Pairwise classification_
    - Build model for each pair of classes, using only training data from those classes
    - Time complexity is not high (small training sets)

## Perceptron

  - No need for probability estimates when only goal is to classify
  - Learning classification
  - **Assumption:** data is linearly separable
  - Algorithm for learning the separating hyperplane
  - If sum > 0, predicts class 1, else other class

  #### Psudocode

  ```
    Set all weights to 0
    Until all instances in training set are classified correctly
      For each instance I in training data
        If I classified incorrectly
          If I belongs to class 1, add weight
          else subtract
  ```

## Winnow

  - _Mistake-driven_ algorithm
    - Assumes binary data
  - Similar to Perceptron
    - Multiplicative rather than additive updates
  - User specified threshold (phi)

  #### Psudocode

  ```
    while some instances are misclassified
      for each instance a in the training data
        classify a using current weights
        if incorrect
          if a belongs to class 1
            multiply wi by alpha IF ai is 1
          else divide wi by alpha IF a1 is 0  
  ```
