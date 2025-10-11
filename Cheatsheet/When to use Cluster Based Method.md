# When to use Cluster Based Method ?

Clustering-based methods for anomaly detection identify outliers by assuming that normal data points belong to large, dense clusters, while anomalies are isolated points that do not belong to any cluster or form very small, sparse clusters.

These methods work by partitioning the data space into groups and measuring how well each point fits into an established group.

## How Clustering-Based Methods Work 🌐
The core idea is to establish what constitutes a "normal neighborhood" in the feature space:

* Clustering: The algorithm (e.g., k-Means or DBSCAN) groups the majority of the data into distinct clusters.
* Anomaly Scoring: For every data point, a score is calculated based on its distance from the center of its nearest cluster, or the density of its local area.
* Flagging: Points with a high distance score (far from any cluster center) or a very low density score (in a sparse area) are flagged as anomalies.

### Key Technique: k-Means Clustering 🖇️
* Mechanism: The data is partitioned into k clusters, with each point assigned to the cluster whose centroid (center) is closest.
* Anomaly Detection: Anomalies are the data points that have a large distance from their assigned cluster centroid. Since anomalies don't fit well with the normal data, the distance between them and the center of their nearest cluster is unusually large.

## When to Use Clustering-Based Methods 🎯
Clustering methods are best used in unsupervised learning scenarios where you have the following conditions:

* No Labeled Anomaly Data: You do not have pre-labeled examples of what constitutes an anomaly, so you must rely on the structure of the normal data to define "abnormal."
* Assumption of Natural Groupings: Your normal data is expected to form clear, separable clusters (e.g., different user segments, distinct machine operational states).
* Global Outliers are the Target: These methods are effective at finding global outliers—points that are significantly far away from the mass of the data. (For local anomalies, Density-Based methods like LOF are often better).
* Moderate Dimensionality: They work well when the number of features (dimensions) is manageable.

## Simple Example: Identifying Unusual Server Load 🖥️
Imagine a monitoring system tracking server behavior based on two variables: CPU Utilization and Memory Usage.

* Normal Clusters: Most of the time, the server operates in two main modes:
  * Cluster 1 (Idle): Low CPU (5-10%) and Low Memory (20-30%).
  * Cluster 2 (Peak): High CPU (70-90%) and High Memory (60-80%).
* k-Means Application: We run k-Means with k=2 to find the centers of these two normal operational clusters.
* Anomaly: A new data point arrives: CPU 85% and Memory 35%.
* Anomaly Flagging:
  * This point is assigned to Cluster 2 (Peak) because the CPU is high.
  * However, the distance from this point to the Cluster 2 centroid (which expects 60-80% memory) is extremely large because the memory usage (35%) is unusually low for such high CPU utilization.
  * The model flags this high distance as an anomaly.
* Implication: This anomaly suggests an unusual operational state—a process is intensely using the CPU but is not loading into memory as expected, perhaps indicating a system resource issue or an application fault.
