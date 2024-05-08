# DSC_clustering_algo_prototype
Step-by-Step Explanation
1. Initialization and Data Preparation:
The model starts by initializing a DataFrame df_original and assigning a unique fam_id to each row. This ID helps in tracking family memberships across iterations.

2. Pairwise Distance Calculation:
It calculates the pairwise Euclidean distances between all data points using their features, ignoring the fam_id during this calculation.

3. Distance Matrix Adjustment:
A matrix that stores these distances is adjusted by setting distances within the same family (fam_id) to infinity, ensuring that no data point is considered its own neighbor.

4. Finding Closest Families:
For each data point, the model finds the closest other data point (in terms of distance) that belongs to a different family.

5. Sorting and Deduplication:
The data points are then sorted based on their distance to these closest other family members. This helps in determining the primary candidates for family reassignment, facilitating a minimal set of migrations to more closely related families.

6. Migration Eligibility and Permissions:
Data points are reassigned to new families based on eligibility criteria derived from their distances to potential new families. Only those closest in distance (and thereby most similar) are allowed to migrate, ensuring the cohesion within families.

7. Union-Find Structure:
A union-find data structure is employed to dynamically manage and merge families based on the migration decisions, allowing for efficient grouping and updating of family memberships.

8. Centroid Calculation and Reassignment:
After each round of migration and family updates, centroids (mean feature vectors) of each family are calculated. Data points are then reassigned to the family whose centroid they are closest to, ensuring families are as internally coherent as possible.

9. Iteration and Convergence:
The model iterates through the above steps multiple times, each time recalculating distances, reassigning families, and updating centroids until a specified condition is met (like a set number of families or convergence of family assignments).

10. Performance Metrics:
During each iteration, the model evaluates the clustering performance using metrics like silhouette score and Calinski-Harabasz score. These metrics help in assessing the quality of clustering, providing insights into the separation between clusters and the tightness of clusters internally.

11. Output and Termination:
The process continues until a pre-defined stopping criterion (like achieving a target number of families) is met. After completion, a summary of performance across iterations is compiled into a DataFrame, showing the evolution of clustering quality and family counts across iterations.

Purpose and Applications
This model is especially suited for dynamic clustering where the goal is not just to group similar entities but also to refine these groups iteratively based on evolving relationships and similarities. This approach can be particularly useful in fields like customer segmentation, anomaly detection, or any scenario where data points can have shifting relationships that need to be captured by the clustering model over time.
