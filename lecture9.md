# Support Vector Machines

## Extending Linear Models

  - Linear models are effective when they are linearly separable
    - By definition: can be separated by a hyperplane
  - Support Vector Machines (SVM) use linear models to implement non-linear classes, by changing input using non-linear mappings

## Non-linear Mapping

  - Example: Going from 2D to 4D using product
    - {a<sub>1</sub>, a<sub>2</sub>} -> {a<sub>1</sub><sup>3</sup>, a<sub>1</sub><sup>2</sup>a<sub>2</sub>, a<sub>1</sub>a<sub>2</sub><sup>2</sup>, a<sub>2</sub><sup>3</sup>}
    - Original dot product
      - x = w **dot** a = w<sub>0</sub>a<sub>0</sub> + w<sub>1</sub>a<sub>1</sub> + w<sub>2</sub>a<sub>2</sub>
    - New space
      - x = w **dot** a = w<sub>0</sub>a<sub>0</sub> + w<sub>1</sub>a<sub>1</sub><sup>3</sup> +  w<sub>2</sub>a<sub>1</sub><sup>2</sup>a<sub>2</sub> + w<sub>3</sub>a<sub>1</sub>a<sub>2</sub><sup>2</sup> +  w<sub>4</sub>a<sub>2</sub><sup>3</sup>
  - New space -> more weights
  - Training becomes infeasible due to amount of weights to be learned
  - SVM reduce problem by finding a maximum margin hyperplane (MMH) as linear model

## Kernel Functions

  - Polynomial kernel (x **dot** y)<sup>n</sup>
  - Other common kernel functions
    - Radial basis function (RBF) _exp(**gamma** || x - y || <sup>2</sup>)_
    - Sigmoid kernel _tanh(kx **dot** y + c)_
  - Best function depends on application, difference is typically small

## SVM in Practice

  - Noise
    - Cann apply SVM to noisy data by introducing a "noise" parameter C
    - C bounds influence of any one training instance to decision boundary
      - Corresponding constraint 0 <= _alpha<sub>i</sub>_ <= C
  - Sparse data
     - SVM algorithms speed up if data is sparse
     - Dot products can be computed  efficiently
     - SVMs can process sparse datasets with 10,000s of attributes
  - Can be modified for numeric prediction - support vector regression

## Perceptron

  - Can use kernel trick to make non-linear classifier using perceptron
  - Can make multilayer perceptron to create a network
    - Example of artificial neural network
