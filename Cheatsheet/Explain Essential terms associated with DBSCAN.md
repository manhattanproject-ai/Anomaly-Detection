# Explain Essential terms associated with DBSCAN

DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is a powerful clustering algorithm that groups together closely packed points, marking points that lie alone in low-density regions as outliers. The following terms are essential to understanding its
mechanism:

<img width="1803" height="807" alt="image" src="https://github.com/user-attachments/assets/a7c901c0-a0f3-4eed-a3f5-8e2390ac7985" />

## 1. Eps (ϵ) (Epsilon) 📏
* Definition: Eps, or Epsilon, is the maximum radius that defines the neighborhood around a given data point.
* Role: If a point A is within the distance ϵ of point B, then A is considered to be a direct neighbor of B. This radius determines how far DBSCAN will look to find neighboring points.

## 2. Min_samples 🔢
* Definition: Min_samples is the minimum number of points (including the point itself) required within the ϵ-neighborhood of a point to consider that point a Core Point.
* Role: This parameter directly controls the minimum density needed to form a valid cluster. A higher value leads to fewer clusters, as only very dense regions will qualify.

## 3. Core Points 🟢
* Definition: A point is a Core Point if its ϵ-neighborhood contains at least Min_samples data points.
* Role: These points are the foundation of a cluster. All points reachable from a Core Point (either directly or indirectly) belong to the same cluster.

## 4. Border Points 🟡
* Definition: A point is a Border Point if it satisfies two conditions:
  * It is within the ϵ-neighborhood of a Core Point.
  * Its own ϵ-neighborhood contains fewer than Min_samples points.
* Role: Border Points are the points that lie on the edge of a cluster. They are considered part of the cluster because they are sufficiently close to a Core Point, but they aren't dense enough to start their own cluster.

## 5. Noise Points (Outliers) 🔴
* Definition: A point is a Noise Point (or Outlier) if it is neither a Core Point nor a Border Point.
* Role: These are the points that lie in low-density regions. They are too far from any Core Point to be considered part of a cluster and are flagged as anomalies. DBSCAN handles noise points naturally without having to define a fixed number of clusters beforehand.
