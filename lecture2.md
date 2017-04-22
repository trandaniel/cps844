# Input and Output

## Terminology

 - **Concept:** Thing to be learned
 - **Concept Description:** Output of learning scheme
 - **Instance:** The individual, independent example of a concept
 - **Attribute (feature):** Measuring aspects of an instance
 - **Input to Learning Scheme:** Set of instances that are described by a predetermined set of attributes - represented as a single relation or file

## How to Learn the Concept

 - **Types of Learning**
   - _Supervised **(training set included)**_
     - Classification
     - Numeric prediction (regression)
   - _Unsupervised **(no training set)**_
     - Association rules
     - Clustering

## Multi-Instance Concept

 - Each individual example comprises a set of instances
   - All instances are described by the same attributes
   - One or more instances may be responsible for its classification
 - Goal of learning is to produce concept description
 - Important real world applications

## Attribute Types

 - **Nominal**
   - Values are distinct symbols
   - No relation among nominal values
   - Only equality test can be performed
   - Example from weather data
   ```
    Attribute: outlook
    Values:    sunny, overcast, rainy
   ```

 - **Ordinal**
   - Impose order on values, no distance between values
   - Addition and subtraction make no sense
   - Example from weather data
   ```
    Attribute: temperature
    Values:    hot > mild > cool
   ```
 - **Interval**
   - Ordered, measured in fixed and equal units
   - Difference of two values makes sense, not sum or product; no zero point defined
   - Example from weather data
   ```
    Attribute: temperature
    Values:    degrees in Fahrenheit
   ```
 - **Ratio**
   - Measurement scheme defines a zero point
   - Treated as real numbers, all math operations are allowed

## Attribute Types in Practice

 - Most schemes accommodate two levels of measurement: nominal and ordinal
 - Nominal (categorial) sometimes referred as enumerated or discrete
   - Enumerated or discrete imply order
   - Special case: dichotomy (boolean)
 - Ordinal values are called numeric or continuous
   - Continuous implies mathematical continuity

## Sparse Data

 - Some applications result in 0 as most values in an attribute
   - e.g. word count in text categorization problem
   ```
    0, 26, 0, 0, 0, 0, 63, 0, 0, 0, class A
    0, 0, 0, 42, 0, 0, 0, 0, 0, 0,  class B

    {1 26, 6 63, 10 class A}
    {3 42, 10 class B}
   ```
   - Also works for nominal values where first attribute is zero

## Missing Values

  - Frequently indicated by out-of-range values
  - Types:
    - Unknown
    - Unrecorded
    - Irrelevant
  - Reasons:
    - Malfunctioning equipment
    - Changes in experimental design
    - Collation of different data sets
    - Measurement is not possible
  - Missing values may have significance
    - Most schemes assume this isn't the case ("missing" as an additional value)

## Inaccurate Values

  - **Reason:** Data was not collected for purpose of data mining
  - **Result:** Errors and omissions that don't affect original purpose of data
  - Typographical errors in nominal attributes -> values need to be checked for consistency
  - Errors may be deliberate (wrong zip code)
  - **Other problems:** Duplicates, stale data

## Getting to Know Your Data

  - Simple visualization tools are useful
    - Histograms for nominal attributes
    - Graphcs for numerical attributes
  - 2D, 3D plots show dependencies
  - Consulting domain experts
  - Too much data -> take sample size

## Output

  - **Output:** Representing structural patterns
    - Decision trees, rules, instance-based, ...
    - "Knowledge" representation
  - Determines inference method
  - Understanding output is the key to understanding underlying learning methods
  - Different types of output for learning problems
    - Classification
    - Regression

## Different Types of Output

  - Tables
  - Linear models
  - Trees
  - Rules
    - Classification
    - Association
  - Instance-based representation
  - Clusters
