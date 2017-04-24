# Data Transformation

## Attribute Selection

  - Adding random attribute can degrade performance of decision trees
  - Instance-based learnings are susceptible to irrelevant attributes
  - Not a problem for NB
  - **Attribute Selection:** Eliminate all but relevant attributes

## Scheme-Independent Attribute Selection

  - **Filter approach:** Assess based on general characteristics of data
  - A method is to find smallest subset of attributes that separates data
  - Or use different learning scheme
    - Attributes selected by C4.5 or 1R
    - Rank attributes by coefficients of linear model, or perform recursive elimination
  - IBL-based attribute weighting techniques
    - Select random instance I = {a, b, c, d, yes}
    - Consider neighbour J = {a, b, c, f, yes}
      - Near hit since similar to I
      - Assume a<sub>4</sub> is irrelevant since same classification (a<sub>4</sub> is not a deciding factor for classification)
    - Consider K = {a, b, c, f, no}
      - Near hit since similar to I
      - a<sub>4</sub> is important since it changed the class
    - Repeat until ordering of importance emerges

## Searching Attribute Space

  - Common greedy approaches
    - Forward selection
    - Backwards selection

##### Forward Selection

```
  start with no attribute in subset S
  run P1 to determine accuracy

  P1:
    generate model using learning algorithm with input as training but only attributes in S measure accuracy with 10foldCV

  Loop:
    consider each attribute not in S as candidate and run P1 by adding attribute to S to check quality
      If no improvement stop and done
      otherwise add attribute that improved accuracy

  returns subset S of attributes
```

##### Backward Selection

  - Forward in reverse lol

```
  start with all attributes in S
  run P1 with each attribute removed
  remove attribute that provided most improvement
  repeat until no improvement
```

  - In general, Backwards is better
  - Forward selection gives better idea of which attributes are important
