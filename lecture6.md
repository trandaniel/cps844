# Instance-based Learning

  - Stores all instances from training set, then given instance a, predicts class based on nearest known class
  - Most popular - euclidian distance
    - Notable: city-block distance
  - Different attributes measured on different scales
  - Nominal attributes typically 1 or 0
  - Common policy for missing values: assume maximally distant (given normalized attributes)

## Finding Nearest Neighbour Efficiently

  - **Simplest:** Linear scan of data
    - Classification time proportionate to product of training set instances and test sets
  - Can be done efficiently using correct data structures

## Building a kD-Tree

  - Stores set of points in k-dimensional space (k attributes)
  - Steps:
    1. Compute variance of attributes in each direction
    2. Choose direction with greatest variance and find median
       - Value closest to mean an be better if skewed data
    3. Median instance becomes root
       - Branches from root, one branch is greater than, other is less than median
    4. Select children nodes and branches in recursive manner (wow recursion)

## Using a kD-Tree to Locate Nearest Neighbour

  - Let instance fall through tree from root node
  - Keep track of nearest neighbour during descent, sets min distance
  - Go back up tree and explore adjoining regions within min distance

## Building Trees Incrementally

  - Big advantage of instance-based learning: classifier is updated incrementally
  - Heuristic strategy to do same with kD-trees

## Multi-instance Learning

  - Typically an instance is a single thing, sometimes group of instances form a unit that is to be classified
  - Machine learning algorithms designed for multi-instance learning
  - Two simple approaches
    - Manipulate input
    - Manipulate output
  - **Bag:** The multiple instance

## Aggregating the Input

  - Convert each bag into a single summary instance

## Aggregating the Output

  - Generate classifier using all training bags converted into training instances 
