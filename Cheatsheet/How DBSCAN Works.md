# How DBSCAN works ?

The working mechanism of DBSCAN can be described in five main steps:

## Step 1. Initialization 🌐

* Explanation: This step involves setting the two critical parameters that the algorithm relies on to define a cluster region: Eps (ϵ), the radius that defines the neighborhood, and Min_samples (the minimum number of points).
* Objective: To establish the minimum density required for a region to be considered a cluster.

## Step 2. Core Point Identification 🌐

* Explanation: The algorithm iterates through every point in the dataset. If a point's ϵ-neighborhood contains at least Min_samples points, it is identified as a Core Point.
* Objective: To identify the dense starting points for cluster construction. Once a Core Point is found, a new cluster is initiated.

## Step 3 Cluster Expansion 🌐
   
* Explanation: From the initial Core Point, the algorithm begins to expand the cluster. It moves to the neighbors and checks their density. Points that are dense enough to become Core Points are added to expand the cluster. Points that are close to a Core Point but not dense enough by themselves are marked as Border Points.
* Objective: To recruit all density-reachable points into the cluster, defining its full extent and shape.

## Step 4. Cluster Completion 🌐

* Explanation: The algorithm continues this expansion process, applying the two rules (Core Point or Border Point) until no more points can be added to the current cluster. All points within the density-reachable region are assigned to the single cluster.
* Objective: To fully delineate one complete, dense cluster.

## Step 5. Iteration 🌐

* Explanation: Once a cluster is fully formed, the algorithm moves to another unclassified point, randomly selecting a point in the dataset to begin and repeat the process from Step 2. This continues until all data points have been visited or assigned a final state (Core, Border, or Noise).
* Objective: To ensure all clusters are found. Points that are visited but remain unassigned (because they are not Core or Border points for any cluster) are classified as Noise Points (Outliers).
