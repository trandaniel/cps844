# Covering Algorithm and Association Rules

## Classification Rules
  - Popular alternative to decision trees
  - **Antecedent (Pre-condition):** a series of tests (e.g. tests at the nodes of decision tree)
  - Test are usually ANDed together (may be general logic expressions)
  - **Consequence (Conclusion):** classes, set of classes, or probability distribution assigned by rule
  - Individual rules are often logically ORed together
    - Conflicts arise if different conclusions apply
  - e.g. If outlook = sunny and humidity = hight then play = no

## Converting Tree to Rules

  - One rule for each leaf
    - Antecedent contains a condition for every node on the path from the root to the leaf
  - Produces rules that are unambiguous
    - Doesn't matter in which order they are executed
  - Resulting rules are unnecessarily complex
    - Pruning to remove redundant tests/

## Rules vs. Decision Tree

  - Advantages of rules over decision trees
    - Sometimes rules form simpler representation of a concept
    - More modular
      - Each rule is independent, can add or remove without disturbing other rules
  - Disadvantages
    - Trees are unambiguous
      - e.g. more than one rule can apply or none

## Interpreting Rules

  - Two types of rule sets
    - Decision list (ordered set of rules)
    - Unordered set of rules - can lead to overlapping and multiple predictions
  - When multiple rules apply (rule A, rule B)
    - Make no prediction
    - Choose rule that applies the most in training set
    - Predict based on ZeroR

## Rules with Exceptions

  - Allow rules to have exceptions

  #### Example

  ```
    iris dataset

    initial rule:
      if petal-length >= 2.45 and petal-length < 4.45 then iris-versicolor

    --------------------------New Instance---------------------
    sepal-length: 5.1
    sepal-width:  3.5
    petal-length: 2.6
    petal-width:  0.2
    Type:         iris-setosa

    modified rule:
      if petal-length >= 2.45 and petal-length < 4.45 then iris-versicolor
      EXCEPT if petal-width < 1.0 then iris-setosa
  ```

## Advantage of Using Exceptions

  - Rules may be updated incrementally
    - Easier to incorporate new data
    - Easier to incorporate domain knowledge
  - We tend to think in terms of exceptions
  - Each conclusion can be considered in just the context
    - Locality is important for large rulesets
    - "Normal" rulesets don't offer this advantage

## Covering Algorithm

  - Convert decision tree to a rule set
    - Rule set overly complex
    - More effective conversions are not trival
  - Generate rule set directly
    - For each class, find rule that covers all instances
  - Covering approach
    - Each stage "covers" some instances

## PRISM Algorithm

  1. Make a rule in form of:
     - if ? then class = a
  2. Select rule that has highest accuracy and remove those instances
  3. Repeat until no more instances of class = a

  #### Psudocode

  ```
    For each class C
      Init E to the instance set
      While E contains instances in class C
        Create rule R with empty left hand side that predicts C
        Until R is perfect (or no attributes) do
          For each attribute A not in R, and each value V,
            Consider condition A = V in left-hand side of R
            Select A and V to maximize accuracy p/t
              (break ties by bigger p)
          Add A = v to R
      Remove instances covered in R from E
  ```

  ## Rules vs Decision List

  - PRISM with outer loop removed generates decision list for one class
    - Subsequent rules are designed for rules not covered previously
    - Order doesn't matter - predicts same class
  - Outer loop considers all classes separately
    - No order dependence implied
    - Results in a rule set
  - **Problems:** Overlapping rules, requires default rule

## Separate and Conquer

  - Like PRISM
    1. **Identify** a rule
    2. **Separate** instances
    3. **Conquer** remaining instances
  - Different from divide and conquer

## Mining Association Rules

  - Predicts any attribute, or combination of attributes based on other attributes
  - Naive method for finding association rules
    - Separate and Conquer
    - Treats every combination of attributes as a different class
  - **Problems**
    1. Computational complexity
    2. Too many rules

## Item Sets

  - **Support (p):** Number of instances correctly covered by association rule (both LHS and RHS)
  - **Confidence (p/t):** Support divided by total number of instances with LHS true measuring accuracy of rule
  - **Item:** one attribute-value pair
  - **Item set:** All items occurring in a rule
    - e.g. {temperature = hot, humidity = high}
  - **Goal:** Only rules that exceed pre-defined support
    - Find all item sets with min support and generating rules from them

## Generating Item Sets Efficiently

  - One-item sets ez
  - **Idea:** Use one-item sets to generate two-item sets ... etc
