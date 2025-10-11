# When to use Classification-Boundary-Based Methods

Classification/Boundary-Based Methods for anomaly detection involve training a model to explicitly define the boundaries of "normal" data. The core idea is to treat anomaly detection as a classification problem where the model learns to distinguish between the typical
data region and the empty, or anomalous, region. Any new data point that falls outside the learned boundary is flagged as an anomaly.

## 🛡️ Key Technique: One-Class SVM (Support Vector Machine)
The most prominent example of a boundary-based method is the One-Class SVM:

* Training: The model is trained only on data that is known to be "normal". Unlike traditional classification, which separates two or more classes (e.g., Cat vs. Dog), One-Class SVM is designed to separate one class (Normal) from everything else.
* Boundary Learning: It learns a hypersphere or boundary in the feature space that encapsulates the vast majority of the normal data points.
* Anomaly Flagging: Any new data point that falls outside this defined boundary is classified as an anomaly.

## 🎯 When to Use Boundary-Based Methods
Boundary-Based Methods, particularly One-Class SVM, should be used in the following scenarios:

* When Anomalous Data is Rare or Non-Existent for Training: These methods are ideal for unsupervised or semi-supervised scenarios where you have a large dataset of normal behavior but very few, if any, known examples of anomalies. Since the model only learns the boundary of the normal class, it doesn't need anomaly examples.
* When the "Normal" Class is Well-Defined: They perform best when the data belonging to the normal class forms a relatively tight, compact cluster in the feature space.
* To Minimize False Negatives on New Data: Once the boundary of normal data is well-established, any deviation beyond it is immediately flagged, making it effective for catching completely novel types of anomalies.

## 💡 Simple Example: Defining Normal Server Load
Scenario: Monitoring Web Server CPU Usage

An IT team wants to monitor a web server to catch sudden, unusual load spikes that might indicate a hacking attempt or a fault.

* Training Data: The model is trained for two weeks on the server's CPU utilization data collected during normal operation (e.g., utilization stays between 20% and 50%). No fault data is included.
* Model Training (One-Class SVM): The One-Class SVM learns the shape of this normal data cluster (the 20%–50% range). It draws an invisible boundary encompassing all points within this typical usage pattern.
* Real-Time Monitoring:
  * Normal Input: CPU usage of 35% comes in. It falls inside the learned boundary → Normal.
  * Anomalous Input: CPU usage spikes to 90%. This point falls outside the learned boundary → Anomaly Flagged.

The model successfully flagged the 90% spike as an anomaly because it violated the learned boundary of what the server's normal behavior is supposed to be.
