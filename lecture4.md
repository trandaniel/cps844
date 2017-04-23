# Covering Algorithm and Association Rules

## Classification Rules
  - Popular alternative to decision trees
  - **Antecedent (Pre-condition):** a series of tests (e.g. tests at the nodes of decision tree)
  - Test are usually ANDed together (may be general logic expressions)
  - **Consequence (Conclusion):** classes, set of classes, or probability distribution assiged by rule
  - Individual rules are often logically ORed together
    - Conflcits arise if different conclusions apply
  - e.g. If outlook = sunny and humidity = hight then play = no
  
## Converting Tree to Rules

  - One rule for each leaf
    - Antecedent contains a condition for every node on the path from the root to the leaf
  - Produces rules that are unambiguous
    - Doesn't matter in which order they are executed
  - Resulting rules are unnecessarily complex
    - Pruning to remove redundant tests/
    
## Rules vs. Decision Tree
 
  - Advantages of rules over decision t ree
    - 
