# Detailed Explanation of DBSCAN

## 🌐 Step 1: Initialization (Setting Critical Parameters)
The first step in the DBSCAN algorithm is to initialize the process by setting the two fundamental parameters that define what constitutes a "dense region" or cluster.

<img width="1199" height="645" alt="image" src="https://github.com/user-attachments/assets/1108d10a-540e-49fb-bfab-dc5d916b7fd5" />

### 1. Select a Radius (ϵ or Eps) 📏
* Action: A value is chosen for the radius (ϵ), which defines the maximum distance a point can be from another point to be considered its direct neighbor.
* Objective: To establish the size of the neighborhood the algorithm will check around every single data point.
* Context Example: The parameter is set to eps = 0.75. This means if the distance between any two points is 0.75 units or less, they are neighbors.

### 2. Select Minimum Number of Points (Min_samples) 🔢
* Action: A value is chosen for Min_samples, which defines the minimum number of points (including the point itself) that must fall within the ϵ-neighborhood for that point to be classified as a Core Point.
* Objective: To establish the minimum density threshold required to form a valid cluster.
* Context Example: The parameter is set to min_samples = 4. Therefore, any point must have at least 4 neighbors within a 0.75 radius to be a Core Point.

By setting these two parameters, DBSCAN establishes a clear, density-based definition of a cluster before the actual grouping process begins.

## 🌐 Step 2: Core Point Identification
This step is where DBSCAN begins iterating through the data to find points dense enough to initiate a cluster, based on the parameters set in Step 1 (eps=0.75, min_samples=4).

The process involves randomly selecting an unclassified point and checking its neighborhood to see if it meets the minimum density requirement.

<img width="1865" height="926" alt="image" src="https://github.com/user-attachments/assets/8dc71908-b8e2-4bbf-9077-8055c6e339d1" />

### 1. Select a Random Unclassified Point
* Action: The algorithm starts by randomly selecting any point in the dataset that hasn't been visited or classified yet.
* Context Example: Let's assume the algorithm picks a point labeled '1' in the dense center of the data.

### 2. Count Neighbors within Epsilon (ϵ)
* Action: The algorithm calculates the distance from the selected point ('1') to all other points. It then counts how many points fall within the defined radius (ϵ=0.75).
* Context Example: When a circle with a radius of 0.75 is drawn around point '1', it is found to contain 5 data points (points 1, 2, 3, 4, and 5).

<img width="1867" height="950" alt="image" src="https://github.com/user-attachments/assets/c8fbe7c0-6d65-4161-96d8-cdfd45f230cc" />

### 3. Core Point Classification
* Action: The count of neighbors is compared against the Min_samples threshold.
* Context Example:
  * The neighbor count is 5.
  * The threshold is min_samples=4.
  * Since 5≥4, point '1' is classified as a Core Point.

### 4. Cluster Initiation
* Action: Once a Core Point is identified, it signals the start of a new cluster. The point is labeled as a Core Point, and all points within its ϵ-neighborhood (its neighbors) are marked as being associated with this nascent cluster.
* Objective: To identify all dense regions that will serve as the seeds for the cluster expansion process.

## 🌐 Step 3: Cluster Expansion
Once a Core Point is identified (Step 2), the algorithm enters the Cluster Expansion phase. The objective is to absorb all points that are density-reachable from that initial Core Point, thereby forming the complete cluster boundary.

<img width="1812" height="848" alt="image" src="https://github.com/user-attachments/assets/5a5d3c7a-8696-45b8-be2e-5c56f7eebfab" />

### 1. Expanding from the Core Point (Seed)
* Action: The algorithm systematically visits the immediate neighbors of the newly classified Core Point (Point 1 from Step 2).
* Context Example (Initial Core Point): Point 1 is a Core Point (min_samples=4 met) and starts Cluster A. Its neighbors (Points 2, 3, 4, 5) are now under investigation.

### 2. Investigating Neighbors of the Core Point (Cluster Growth)
The algorithm checks each neighbor to determine if it is dense enough to be a new Core Point, which would continue the expansion, or if it's merely a Border Point.

* Action (Checking Neighbor 2): The algorithm moves to Neighbor 2 and counts the points within its ϵ-radius.
* Context Example (Neighbor 2 Check):
  * Draw a circle with eps=0.75 around Point 2.
  * Assume this neighborhood contains 5 points (Points 1, 2, 3, 4, and 5).
  * Since 5≥min_samples=4, Point 2 is also classified as a Core Point.
  * Point 2's unclassified neighbors are now added to the list of points to check, further expanding Cluster A.

<img width="1836" height="874" alt="image" src="https://github.com/user-attachments/assets/886799d7-e822-49e1-87e3-477166260b4c" />

### 3. Identifying Border Points (Edge of Cluster)
* Action: The expansion continues until a neighbor is found that is within the radius of a Core Point, but is not dense enough to be a Core Point itself.
* Context Example (Neighbor 3 Check):
  * The algorithm moves to Neighbor 3.
  * Draw a circle with eps=0.75 around Point 3.
  * Assume this neighborhood contains only 3 points.
  * Since 3<min_samples=4, Point 3 is not a Core Point.
  * However, because Point 3 is directly reachable by a Core Point (Point 1), it is classified as a Border Point and is assigned to Cluster A.

<img width="1193" height="551" alt="image" src="https://github.com/user-attachments/assets/e38174d7-b6c5-4b16-ae01-0f1f30bb863f" />

### 4. Noise Point Classification
* Action: A point is classified as a Noise Point if it is neither a Core Point nor a Border Point.
  * It fails the Core Point test (insufficient neighbors).
  * It fails the Border Point test (it is not within the ϵ-neighborhood of any established Core Point).
* Context Example:
  * Point 1 is not dense enough to be a Core Point.
  * Point 1 is too far away from the Core Points of the previous cluster (Cluster A) to be classified as a Border Point.
  * Conclusion: Point 1 is labeled as a Noise Point (Outlier) and is not assigned to any cluster.

## 🌐 Step 4: Cluster Completion (Labeling All Points)
The Cluster Completion step is the final phase of defining a single cluster. The algorithm continues the expansion process from all current Core Points until every density-reachable point has been assigned to the cluster, and no further expansion is possible.

<img width="1216" height="600" alt="image" src="https://github.com/user-attachments/assets/3407b279-6628-46c6-92b1-67543aff631f" />

### 1. Continuous Expansion and Checking
* Action: The process from Step 3 continues recursively: the algorithm moves from one Core Point to its neighbors, checks if those neighbors are dense enough to be new Core Points, and adds all reachable Border Points to the cluster.
* Objective: To ensure that the maximum contiguous dense region (the cluster) is entirely encompassed and labeled.
* Context Example (Iteration): The algorithm continues expanding from new Core Points (like Point 2 in the example) and any other Core Points found. As shown in the image, many more points are now labeled in teal (cyan), indicating they are part of the growing cluster (Cluster A).

<img width="1193" height="596" alt="image" src="https://github.com/user-attachments/assets/fc03ab03-76da-4382-a940-b76a99230890" />

### 2. Stopping Condition
* Action: The expansion stops when all unclassified points within the ϵ-neighborhoods of the Core Points have been visited, and no point can be found that meets the Min_samples criterion to become a new Core Point that could extend the cluster.
* Result: All points connected by density-reachability (a chain of Core Points) are now labeled with the same cluster ID (e.g., Cluster A).

## 🌐 Step 5: Iteration (Finding All Clusters and Outliers)
The final step of DBSCAN is the Iteration phase, where the algorithm systematically ensures that every data point has been visited and assigned to a cluster or classified as noise.

<img width="1839" height="902" alt="image" src="https://github.com/user-attachments/assets/5c11a864-0d21-43ce-8ad8-d5bce77c422f" />

### 1. Moving to the Next Unclassified Point
* Action: Once the initial cluster (Cluster A) is fully complete (all density-reachable points are labeled), the algorithm selects the next available unclassified point at random and begins the process again from Step 2 (Core Point Identification).
* Objective: To find any other dense regions that form distinct clusters.

### 2. Repeating the Process (Finding Cluster B)
* Action: The ϵ-neighborhood of the newly selected point (Point 1 in the new region, image image_b951d4.png) is checked against the min_samples threshold.
* Context Example (Finding Cluster B): In the top-right region of the dataset, a new point is selected and found to have 6 neighbors (≥min_samples=4). This point becomes a new Core Point, initiating Cluster B (colored yellow/orange in the final image).
* Result: Cluster B is then expanded and completed, just like Cluster A.

<img width="1864" height="974" alt="image" src="https://github.com/user-attachments/assets/9b770a20-fe4e-49f7-bbb2-37527d37f7ab" />

### 3. Identifying Final Noise Points (Outliers)
* Action: After all dense regions have been identified and grouped into clusters (e.g., Cluster A and Cluster B), any remaining unclassified points are designated as Noise Points.
* Context Example (Final State): As shown in the final visualization, the four black-colored points are the remaining unclassified points. They are in low-density regions, are not density-reachable from any Core Point, and are thus labeled as 4 outliers.
* Objective: To naturally separate the sparse anomalies from the meaningful clusters, completing the analysis.

The entire process terminates when every single data point in the entire dataset has been labeled as either a Core Point, a Border Point, or a Noise Point. 
