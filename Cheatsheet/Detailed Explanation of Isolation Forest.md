# Detailed Explanation of Isolation Forest

## Dataset used for Explanation

<img width="1766" height="808" alt="image" src="https://github.com/user-attachments/assets/12138e49-ffcb-4b4f-a679-9fb9b5cd61be" />

Column Name	Description	Data Type Example
name	The student's name (key identifier)	Text (e.g., "Aaliyah")
books	Time spent reading books weekly (in hours)	Float (e.g., 0.5)
tv_shows	Time spent watching TV shows weekly (in hours)	Float (e.g., 4.6)
video_games	Time spent playing video games weekly (in hours)	Float (e.g., 4.9)


## 🌲 Step 1: Recursive Partitioning (Building the Isolation Tree)
The first step in Isolation Forest is the recursive, random process of building a single Isolation Tree (iTree). The objective is to rapidly separate individual data points from the rest of the dataset.

<img width="1890" height="871" alt="image" src="https://github.com/user-attachments/assets/91125373-3fe5-4449-b2ab-c30f9df59893" />


### Random Feature Selection
* Action: The algorithm randomly selects one of the available features (columns) in the dataset to perform a split.
* Context Example: Given the student dataset, the algorithm randomly chooses one of the three features: Books, TV Shows, or Video Games.

### Random Split Point (Threshold) Selection
* Action: Once a feature is selected, a random split value (or threshold) is chosen that lies between the maximum and minimum values of that feature in the current subset of data.
* Context Example:
  * If the algorithm selected the TV Shows feature, it might observe that the range of all values is between 3.8 and 4.6 (from the top 10 rows).
  * It then randomly chooses a split point within that range, for example, 3.6 hours.

### Partitioning the Data
* Action: All data points are split into two child nodes based on the chosen random threshold.
  * Points with a feature value less than the threshold go to the left branch.
  * Points with a feature value greater than or equal to the threshold go to the right branch.
* Context Example (The Anomaly):
  * Using the threshold of 3.6 hours for the TV Shows feature, all students who watch less than 3.6 hours go left, and the rest go right.
  * If a student, say Alan, watches 2.5 hours of TV, and no other student watches that little, that single data point will be isolated in the left branch with only one split. This point is quickly isolated because it is an anomaly.

### Stopping Condition (Recursion)
* Action: This process of random selection and splitting is repeated recursively on the resulting child nodes until one of the following conditions is met:
  * The node contains only one data point (the point is isolated).
  * The node contains all data points from the initial set (which means the split was not useful).
  * The tree reaches a predefined maximum height (to prevent overfitting).

The crucial insight is that anomalies, being sparse and far from the main cluster of data, will be separated into their own branch much faster than normal data points. Normal data points, being highly clustered, require many more random splits before they are finally isolated.

## 🌲 Step 2: Isolation Tree Construction (Path Length)
This step continues the recursive partitioning begun in Step 1, iteratively isolating all data points and determining their path length. The core objective is to identify short path lengths, as these are the defining characteristic of an anomaly.

<img width="1890" height="1018" alt="image" src="https://github.com/user-attachments/assets/83873ad9-bb65-4d4d-9b2a-fd9b28ae1511" />


### Continuing the Recursive Partitioning
* Action: The splitting process (randomly choosing a feature and a random threshold) continues on the subsets of data in the child nodes.
* Context Example (Branch 1 - TV Shows < 3.6 hours):
  * The leftmost node already contains only a single data point (e.g., Alan, with 2.5 hours of TV).
  * Result: The point is isolated, and the splitting stops for this branch. The path length (number of splits) is 1. This point is considered a likely anomaly.

### Splitting the Remaining Cluster (Normal Data)
* Action: The large cluster of normal data (TV Shows ≥3.6 hours) is split again, using a new randomly selected feature and threshold.
* Context Example (Second Split):
  * The algorithm might randomly select the Books feature.
  * It then selects a random split point, for example, 0.7 hours.
  * Result: Students who read less than 0.7 hours go left, and the rest go right. This isolates a second point (e.g., Abigail, who reads 0.0 hours).
  * Path Length: This second point is isolated after 2 splits (1 for TV Shows, 1 for Books). This point is also a likely anomaly.

### Isolation and Path Length
* Definition of Isolation: Isolation is achieved when a node contains only one data point.
* Path Length: The total number of splits required to isolate a point is its path length.
* Key Insight: Anomalies have a significantly shorter path length because they are sparse and require fewer random partitions to be separated from the rest of the data. Normal points are highly clustered and require many splits—resulting in a long path length—before they are finally isolated.

### Termination Condition
* Action: The splitting continues until every data point is isolated or a predefined maximum depth is reached (e.g., a maximum number of splits, such as 3 in the image).

By the end of this step, every data point in the entire dataset has a path length (a numerical measure of its "anomalousness") within this single Isolation Tree.

## 🌲 Step 3: Ensemble Creation (Building the Forest)
The goal of Isolation Forest is not to rely on a single, potentially biased tree, but to leverage the collective power of many randomized trees. The process of Ensemble Creation involves building a multitude of these Isolation Trees (iTrees) to form the complete
Isolation Forest.

###  Why an Ensemble is Necessary ?
* A single Isolation Tree is highly dependent on the random feature and random threshold selected at each split. If, by chance, the initial splits are poor, the resulting path lengths may be misleading.
* Objective: The ensemble approach averages out the bias and reduces the variance introduced by the random selection process. The final result is far more robust and accurate.

###  The Process of Building the Forest
* Action: Steps 1 and 2 (Recursive Partitioning and Isolation) are repeated a fixed number of times (e.g., typically 100 or 256 times). Each repetition generates a new, independent Isolation Tree.
* Randomization: Crucially, each tree is built using a random subsample of the original data and, at each split, the feature and threshold are again chosen randomly.

### Different Path Trajectories
The randomness ensures that each data point follows a unique path through every tree in the forest.

#### Example Trajectory 1 :

<img width="1213" height="526" alt="image" src="https://github.com/user-attachments/assets/00b6d517-24a7-476e-9d7c-a335cfdee4d4" />

* Split 1: Uses the Books feature.
* Split 2: Uses the Books feature again.
* Split N: Finally uses the TV Shows feature to isolate the point.

#### Example Trajectory 2 :

<img width="1416" height="701" alt="image" src="https://github.com/user-attachments/assets/b128c23c-a31e-4988-84d3-ae05ed14caaf" />

* Split 1: Uses the TV Shows feature.
* Split 2: Uses the Books feature.
* Split N: Uses the Video Games feature to isolate the point.

#### Example Trajectory 3 :

<img width="1124" height="528" alt="image" src="https://github.com/user-attachments/assets/876d6ec2-ec51-407c-8a0e-1550b971d7a3" />

* Split 1: Uses the Video Games feature.
* Split 2: Uses the TV Shows feature.
* Split N: Finally uses the Books feature.

#### Repeat using different features and splits to create multiple trees

<img width="1204" height="784" alt="image" src="https://github.com/user-attachments/assets/e246b6ce-5da5-412d-969d-d2ebc6cb2b3c" />

## 🌲 Step 4: Anomaly Score Calculation
This final step leverages the collection of path lengths generated in the ensemble to calculate a single, normalized Anomaly Score for every data point. This score determines the likelihood that an observation is a true anomaly.

<img width="1891" height="1031" alt="image" src="https://github.com/user-attachments/assets/e2c70519-220b-4714-af97-64679c99565f" />

### Averaging the Path Lengths
* Action: For a single data point (e.g., student Aaliyah), the algorithm collects the path length it took to isolate that point in every single tree of the Isolation Forest.
* Calculation Example: As shown in the image, a single data point's path lengths across four trees might be:
  * Tree 1: 1 split
  * Tree 2: 3 splits
  * Tree 3: 2 splits
  8 Tree N (Tree 4): 1 split

Result: The Average Path Length is calculated: (1+3+2+1)/4=7/4=1.75.

### Normalization and Final Score
* Action: The calculated Average Path Length is then normalized using a specific formula. This formula compares the average path length of the observation against the average path length of a standard, normal point in a binary tree of the same size.
* Objective: This normalization converts the raw path length into a standardized Anomaly Score (S) that always falls between 0 and 1.

### Interpreting the Anomaly Score
The resulting score directly reflects the point's distance from the bulk of the data:
  * Score Close to 1 (e.g., 0.95): The point's average path length is very short. This indicates the point is likely an anomaly (or Global Outlier).
  * Score Around 0.5 (e.g., 0.45 – 0.55): The point's average path length is close to the average for a normal observation. This indicates the point is likely normal and well within the data cluster.
  * Score Close to 0 (e.g., 0.1): The point's average path length is very long. This indicates the point is highly unlikely to be an anomaly.

In the example calculation, the average path length of 1.75 is extremely low, and the final normalized score would be close to 1, confirming that this value is likely an anomaly.

Anomaly Score is the inverse of the Path Length, which is the core concept of Isolation Forest. Let's clarify why a short path length results in a score close to 1.

### The Inverse Relationship: Path Length vs. Anomaly Score
The goal of Isolation Forest is to use as few random splits as possible to isolate an observation. The resulting Anomaly Score (S) is calculated using a formula that effectively converts the path length (h(x)) into a probability-like score ranging from 0 to 1.

Metric	Value	Interpretation	Anomaly Likelihood
Path Length (h(x))	Very Short (e.g., 1.75)	Isolated quickly, close to the root of the tree.	High ⬆️
Anomaly Score (S)	Close to 1 (e.g., 0.95)	This point is very different from the surrounding data.	High ⬆️

#### Why Short Path Length = High Anomaly Score (≈1) 🌲
* Logic: Anomalies are sparse and rare, meaning a random split will likely separate them from the main cluster almost immediately. They fall to the leaf node in a shallow part of the tree.
* Result: The average path length is short. Since the formula is designed to give the highest score (closest to 1) to the shortest path, a low path length confirms the point is a strong anomaly.
* Example: In your calculation, an average path length of 1.75 is extremely short, leading to a normalized score ≈1.

### Why Long Path Length = Normal Score (≈0.5) or Less
* Logic: Normal data points are clustered and dense. To isolate a point within a dense cluster, the algorithm must perform many sequential random splits. They fall to a leaf node in a deep part of the tree.
* Result: The average path length is long. This long path length is normalized to a score around 0.5 (which is the expected score for a non-anomalous point) or sometimes even closer to 0.
* Interpretation: A score of 0.5 means the point is behaving like a typical, normal observation in the dataset.

The rule of thumb is: The easier it is to isolate a point (shorter path), the more anomalous it is (higher score).
