# Different Anomaly detection Technique

Anomaly detection techniques are diverse and are typically categorized based on the underlying model's approach to learning "normal" data and identifying deviations.

Here are the different types of anomaly detection techniques:

## 1. Statistical Methods 📊
These are basic, model-free techniques that assume normal data follows a known statistical distribution (like a Gaussian distribution). Anomalies are points that fall far outside the expected range.

### Z-score / Standard Deviation: 📏
* Technique: Calculates how many standard deviations a data point is from the mean. Any point exceeding a predetermined threshold (e.g., 3σ) is flagged as an anomaly.
* Best for: Univariate data where the distribution is roughly Gaussian.

### Box Plots / IQR (Interquartile Range): 📦
* Technique: Uses the IQR (the range between the 75th and 25th percentiles). Anomalies are defined as points that lie beyond 1.5×IQR below the first quartile or above the third quartile.
* Best for: Univariate, non-Gaussian data, as it is robust to extreme outliers.

## 2. Density-Based Methods 🧭
These methods define anomalies based on how isolated a data point is from its neighbors. Points in sparse regions are considered outliers.

### LOF (Local Outlier Factor): 🏘️
* Technique: Measures the local density of a point compared to the local densities of its neighbors. A point whose density is significantly lower than its neighbors is flagged as an anomaly. This is excellent for detecting local anomalies, where a point might be an outlier compared to its immediate cluster, even if it's not far from the global average.

### k-Nearest Neighbors (k-NN): 
Technique: Flags a data point as an anomaly if the distance to its kth nearest neighbor is unusually large. It relies purely on the distance in the feature space.

## 3. Clustering-Based Methods 🌐
Clustering methods group similar data points together. Anomalies are points that do not belong to any cluster or form very small, sparse clusters.

### k-Means Clustering: 🖇️
* Technique: Clusters the data into k groups. Data points that are far from any cluster centroid (i.e., having a large distance to their assigned cluster center) are marked as outliers.

### DBSCAN (Density-Based Spatial Clustering of Applications with Noise): ⛰️
* Technique: Identifies dense regions of data and marks points that fall outside these regions as noise or outliers. It is effective at identifying irregularly shaped clusters and naturally flags isolated points as anomalies.

## 4. Classification/Boundary-Based Methods 🛡️
These methods involve training a model to explicitly define the boundaries of normal data. Anything outside the learned boundary is anomalous.

### One-Class SVM (Support Vector Machine): 🧤
* Technique: This is trained only on "normal" data. It learns a hypersphere or boundary that encompasses the vast majority of the normal data points. Any new data point falling outside this boundary is flagged as an anomaly.
* Best for: Situations where anomalous data is rare or unavailable for training.

## 5. Machine Learning and Deep Learning Methods 🧠
These advanced techniques are highly effective for complex, high-dimensional, and time-series data, particularly for detecting contextual and collective anomalies.

### Isolation Forest: 🌲
* Technique: Uses decision trees to "isolate" outliers. Since anomalies are few and different, they are easier to separate from the rest of the data and tend to be closer to the root of the tree. The technique measures how quickly a point can be isolated.
* Best for: High-volume data, as it is computationally efficient.

### Autoencoders (Neural Networks): 🔄
* Technique: A type of neural network trained to reconstruct its input data. It is trained only on "normal" data. When a normal instance is fed in, the reconstruction error is low. When an anomaly is fed in, the network struggles to reconstruct it (high reconstruction error), and the high error signals an anomaly.
* Best for: Unsupervised detection in complex, high-dimensional data (e.g., image, log files).

### Recurrent Neural Networks (RNNs) / LSTMs: 📈
* Technique: Used for time-series and sequential data to detect collective anomalies. The network is trained to predict the next value in a sequence. If the actual value deviates significantly from the network's prediction, it suggests a disruption in the expected pattern of the time series.
* Best for: Predicting and flagging deviations in system performance, stock prices, or sensor readings.
