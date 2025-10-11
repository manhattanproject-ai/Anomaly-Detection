# How Isolation Forest Works ?

The algorithm's inner workings are described by the following processes :

## Step 1 : Recursive Partitioning (Isolation): 🌲

* The core process is building isolation trees (iTrees) through recursive partitioning.
* The algorithm randomly selects a feature and then randomly selects a split value between the maximum and minimum values of the selected feature.
* This partitioning process is repeated recursively, effectively creating a binary search tree until the data is fully isolated or the tree reaches a set height limit.

### Objective : To rapidly separate individual data points from the rest of the dataset. Because anomalies are sparse, they will land on their own branch closer to the root of the tree, requiring fewer partitions.

## Step 2 : Isolation (Path Length): 📏

* Outliers, being far from the dense clusters of normal points, generally require fewer partitions (splits) to be separated, resulting in a shorter path length from the root of the tree.
* Normal points, being close to many other data points, require many more partitions, resulting in a longer path length.

### Objective : To quantify how easily a data point can be separated. A shorter path length is the primary indicator of an anomaly.

## Step 3 : Ensemble Function (Building the Forest): 🌳

* The algorithm constructs an ensemble (a collection) of isolation trees.
* The final anomaly score is determined by averaging the path length for each data point across all trees in the ensemble. The use of multiple trees helps ensure the results are robust and not dependent on a single random split.

### Objective : To reduce the effect of randomness and enhance the robustness and accuracy of the final anomaly detection score.

## Step 4 : Anomaly Score Calculation: 🔢

* The final anomaly score for each point is calculated based on the average path length it took to isolate the point across the ensemble of trees.
* A shorter average path length yields a higher anomaly score, indicating that the point is likely to be an anomaly. Conversely, a longer path means a point is normal.

### Objective: To produce a final score. A score closer to 1 indicates a higher probability of the point being an anomaly (due to a significantly shorter average path length), while a score closer to 0.5 indicates the point is likely normal.
