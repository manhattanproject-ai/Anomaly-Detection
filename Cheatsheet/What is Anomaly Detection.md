# What is Anomaly Detection ?

<img width="512" height="341" alt="image" src="https://github.com/user-attachments/assets/6cb00367-571c-4b4b-bc54-0f7d963bfd30" />


Anomaly detection, also known as outlier detection, is the process of identifying data points, events, or observations that deviate significantly from the expected pattern or typical behavior of a dataset. These deviations are referred to as anomalies or outliers.

The primary goal of anomaly detection is to flag unusual occurrences that may indicate a critical event, a problem, an error, or a rare phenomenon requiring investigation.

## 🛠️ Key Concepts

* Anomalies: Data points that do not conform to an expected pattern. They can be classified into three main types:
  * Point Anomalies (Outliers): A single data instance that is abnormal with respect to the rest of the data. (e.g., A transaction for $5,000 when the average is $50).
  * Contextual Anomalies: A data instance that is abnormal only in a specific context. (e.g., A temperature of 30°C in the summer is normal, but a temperature of 30°C in the winter is an anomaly).
  * Collective Anomalies: A collection of related data instances that, taken together, are anomalous, even though each individual instance may not be. (e.g., A sequence of many small, low-value network connections that, when analyzed as a group, indicate a distributed
  denial-of-service (DDoS) attack).
* Normal vs. Anomalous: Anomaly detection models are often trained on large amounts of "normal" data to establish a baseline of expected behavior. Anything that falls outside the defined range or probability of this baseline is marked as anomalous.

## 🎯 Common Applications
Anomaly detection is used across various real-life domains:

* Financial Fraud Detection: Identifying unusual credit card transactions, large money transfers, or inconsistent spending patterns.
* Intrusion Detection: Flagging unusual network traffic or system login attempts that may signify a cyberattack or security breach.
* Manufacturing Quality Control: Detecting defects in products (e.g., machinery vibrations, heat signatures, or assembly errors) that fall outside acceptable manufacturing tolerances.
* Healthcare: Identifying unusual patient symptoms, vital signs, or lab results that could indicate a severe or rare medical condition.
* Time Series Monitoring: Monitoring sensor data from equipment (e.g., servers, engines, or turbines) to predict failures by flagging abnormal readings like sudden temperature spikes or unusual drops in pressure.

## Visualization 

<img width="1346" height="690" alt="image" src="https://github.com/user-attachments/assets/d70023ce-fcce-4d06-ae3b-6463ec22466f" />




