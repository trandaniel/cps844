# 1R, Naive Bayes, and Decision Trees

## Example Data Set

  - Classifies from weather if conditions are good to play golf

_Taken from weather.arff_

| No. | outlook  | temperature | humidity | windy | play |
| --- |:--------:|:-----------:|:--------:|:-----:|:----:|
| 1   | sunny    | hot         | high     | FALSE | no   |
| 2   | sunny    | hot         | high     | TRUE  | no   |
| 3   | overcast | hot         | high     | FALSE | yes  |
| 4   | rainy    | mild        | high     | FALSE | yes  |
| 5   | rainy    | cool        | normal   | FALSE | yes  |
| 6   | rainy    | cool        | normal   | TRUE  | no   |
| 7   | overcast | cool        | normal   | TRUE  | yes  |
| 8   | sunny    | mild        | high     | FALSE | no   |
| 9   | sunny    | cool        | normal   | FALSE | yes  |
| 10  | rainy    | mild        | normal   | FALSE | yes  |
| 11  | sunny    | mild        | normal   | TRUE  | yes  |
| 12  | overcast | mild        | high     | TRUE  | yes  |
| 13  | overcast | hot         | normal   | FALSE | yes  |
| 14  | rainy    | mild        | high     | TRUE  | no   |

## ZeroR - lmao

  - Predicts majority class from the training set
    - Correctly classified   (yes) instances 9 ~= 64%
    - Incorrectly classified (no)  instances 5 ~= 36%

  - ZeroR predicts yes (majority class)

## OneR - meh

  - Learns a 1-level decision tree
    - i.e. rules that all test one particular attribute
  - **Basic version:**
    - One branch for each value
    - Each branch assigns most frequent class
    - **Error rate:** proportion of instances that don't belong to the majority class of their corresponding branch
    - Chooses attribute with lowest error
    - _Assuming nominal attributes_
    - **Note:** "missing" is treated as separate attribute value
  ```
    for each attribute X
      for each value xi of X make a rule:
        count how often each class appears when X = xi
        find most frequent class C
        make a rule: if X = xi, then class = C
      calculate error rate of n rules, where n are values of X
    return rule set with least errors
  ```
  | Attributes   | Rules           | Errors | Total Errors |
  |:------------:|:---------------:|:------:|:------------:|
  | **Outlook**  | Sunny    -> No  | 2/5    | 4/14 *       |
  |              | Overcast -> Yes | 0/4    |              |
  |              | Rainy    -> Yes | 2/5    |              |
  | **Temp**     | Hot*     -> No  | 2/4    | 5/14         |
  |              | Mild     -> Yes | 2/6    |              |
  |              | Cool     -> Yes | 1/4    |              |
  | **Humidity** | High     -> No  | 3/7    | 4/14 *       |
  |              | Normal   -> Yes | 1/7    |              |
  | **Windy**    | False    -> Yes | 2/8    | 5/14         |
  |              | True*    -> No  | 3/6    |              |
  - _Ties broken arbitrarily_
  - **OneR** predicts:
    - If outlook = sunny, then **play = no**
    - If outlook = overcast, then **play = yes**
    - If outlook = rainy, then **play = yes**

## Discretizing Numeric Attributes

  - Sometimes want numeric values in ranges
  - Divide range into intervals
    - Sort instances according to values
    - Place breakpoints where there is a class change
    - Minimizes total error
  - Using temperature from weather data set as example

  |    |    |    |    |    |    |    |    |    |    |    |    |    |    |
  |----|----|----|----|----|----|----|----|----|----|----|----|----|----|
  | 64 | 65 | 68 | 69 | 70 | 71 | 72 | 72 | 75 | 75 | 80 | 81 | 83 | 85 |
  | Y  | N  | Y  | Y  | Y  | N  | N  | Y  | Y  | Y  | N  | Y  | Y  | N  |

  - Add breakpoints when there is a change in class
    - If temperature is constant but there is change in class, shift breakpoint to the right

  |  > | <> | <  |    |  > | <  |    |  > | <  |  > | <> | <> |  > | <  |
  |----|----|----|----|----|----|----|----|----|----|----|----|----|----|
  | 64 | 65 | 68 | 69 | 70 | 71 | 72 | 72 | 75 | 75 | 80 | 81 | 83 | 85 |
  | Y  | N  | Y  | Y  | Y  | N  | N  | Y  | Y  | Y  | N  | Y  | Y  | N  |

  - **Breakpoints:** 64.5, 66.5, 70.5, 73.5, 77.5, 80.5, 84

  - Sensitive to noise
  - Solution -> enforce a minimum number of instances in majority class per interval
    - e.g. min = 3
  - Division in class where,
    - There is change in class
    - At least three instances of majority class
    - If class changes when temperature is constant, shift division to right
    - Merge groups with same majority class

  |    |    |    |    |    |    |    |    |    |  > | <  |    |    |    |
  |----|----|----|----|----|----|----|----|----|----|----|----|----|----|
  | 64 | 65 | 68 | 69 | 70 | 71 | 72 | 72 | 75 | 75 | 80 | 81 | 83 | 85 |
  | Y  | N  | Y  | Y  | Y  | N  | N  | Y  | Y  | Y  | N  | Y  | Y  | N  |

  - **Breakpoint:** 77.5
    - If temp <= 77.5, then yes
    - If temp >  77.5, then no

## Simple Statistical Modelling

  - Uses all attributes
  - Assumes the following:
    - Attributes are equally important
    - Attributes are statistically independent (given class value) - never correct lmao

### Naive Bayes

  - For each attribute, consider how often attribute has given value
    - e.g. from weather data
      - outlook = sunny when play = yes, 2 times
      - outlook = sunny when play = no , 3 times
      - outlook = overcast when play = yes, 4 times
      - ...
    - For all attributes

### Bayes' Rule

  - Probability of an event (hypothesis) H given evidence E
    - Basically multiply all probabilities together
    - e.g. Predict class of a sunny, hot, high, windy day
      - P(sunny | yes) * P(hot | yes) * P(high | yes) * P(windy | yes) * P(yes)
      - Then find P(no) add together and find overall probability

### Zero Frequency Problem

  - Happens when theres 0 frequency for one event
    - Causes calculation to turn out to 0 or 1
  - Fix by adding Laplace Estimator to every instance (usually 1)

### Missing Values

  - Just skip it during calculations lol

## Constructing Decision Trees

  - Strategy: top-down
    - Recursive divide and conquer fashion
  - First: select attribute for root node
    - Create branch for each possible value
  - Split instances into subsets
    - One for each branch extending into node
  - Repeat recursively for each branch using instances that only reach the branch
  - If all instances have the same class for that branch stop developing that part of the tree

  - Add some example here blah
