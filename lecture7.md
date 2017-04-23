# Clustering

  - Applies when there is no class to be predicted
  - **Aim:** Divide instances into natural groups
  - Clusters can be:
    - Disjoint vs. Overlapping
    - Deterministic vs. Probabilistic
    - Flat vs. Hierarchical
  - Four types:
    - Non-overlapping
    - Fuzzy
    - Overlapping
    - Dendrogram

## k-Means Clustering

  - Choose a value k, where k is the number of clusters
  - Choose k random points and the starting centers of clusters
  - Loop through steps until centers have stabilized
    - Assign instance to nearest center
    - Recalculate centroid of each clusters new center

## Convergence Criterion

   - Calculate distance by euclidean distance
   - Stop when there is no minimum change in SSE (sum of squared error of distances)
   - Guaranteed to converge since,
     - Recentering decreases SSE
     - Regrouping decreses SSE
     - Finite number of groupings

## k-Means ++

  - Improves original k-means by choice of initial centers
  - Choose initial seed at random, uniform probability distribution
  - Second seed with probability proportionate to square distance of first
  - Repeat
