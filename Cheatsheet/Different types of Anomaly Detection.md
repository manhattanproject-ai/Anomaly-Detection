# Different types of Anomaly Detection ?

Anomaly detection identifies data points that deviate significantly from expected patterns, and these anomalies are classified into distinct types based on how they manifest within the data.

<img width="966" height="420" alt="image" src="https://github.com/user-attachments/assets/c5d93623-d2d2-4400-9033-00bbe55e8077" />

## 1. Point Anomalies (Outliers) 🚨
Point anomalies occur when a single data instance deviates significantly from the expected range of values. They are typically the easiest to detect but can signal serious, immediate events.

### Detailed Example: Financial Fraud Detection
Scenario: A bank customer, Sarah, typically makes online purchases ranging from $20 to $150. Her average transaction is $75.

* Anomaly: A single transaction appears on her account for $4,800 at an electronics store she has never visited.
* Classification: This is a Point Anomaly because the single value ($4,800) is a massive, sudden deviation from her established financial baseline (typical spending of $20–$150).
* Implication: This single unusual transaction immediately signals potential credit card fraud.
* Detection Challenge: This anomaly could be masked by noisy data if, for example, the bank processes hundreds of thousands of varied transactions per second, requiring accurate thresholding.

## 2. Contextual Anomalies 📅
Contextual anomalies are only identifiable when a data point is viewed within its specific context (e.g., time, location, or user profile). A value that is normal in one setting may be highly unusual in another.

### Detailed Example: Energy Management
Scenario: A regional utility company monitors electricity consumption for a manufacturing plant.

* Normal Context: Between 9:00 AM and 5:00 PM (peak daytime hours), the plant's electricity usage naturally spikes to 80% of its capacity due to machinery operation. This is normal.
* Anomaly: At 3:00 AM (off-peak context), the monitoring system registers an identical 80% surge in electricity usage.
* Classification: This is a Contextual Anomaly because the value (80% usage) is normal during the day but is highly abnormal for 3:00 AM.
* Implication: The spike at 3:00 AM suggests abnormal equipment behavior (e.g., a massive machine was left running, a system glitch occurred, or a fault caused a power drain).
* Detection Challenge: The anomaly detection model must incorporate the time-of-day variable—the context—not just the raw usage percentage.

## 3. Collective Anomalies 🧩
Collective anomalies arise when a group of data points appears normal individually but becomes suspicious when considered as a whole sequence or cluster. The irregularity lies in the pattern, not the individual point.

### Detailed Example: Cybersecurity
Scenario: A company uses a cybersecurity system to monitor login attempts to its internal server for an employee named Tom.

* Individual Data Points:
  * Attempt 1: Login from San Francisco, USA. Normal.
  * Attempt 2: Login from London, UK. Normal.
  * Attempt 3: Login from Tokyo, Japan. Normal.
* Anomaly: All three successful login attempts occur within a five-minute window.
* Classification: This is a Collective Anomaly because each individual login location is plausible for a traveling employee, but the sequence of successful logins from three distinct global locations within minutes is physically impossible for one person.
* Implication: This pattern suggests a coordinated attack or a compromised account being used simultaneously by multiple malicious actors.
* Detection Challenge: Identifying this requires models capable of analyzing the sequence and cluster of data points (e.g., time-series analysis or sequence-aware models) rather than flagging any single data point.


<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/46cdb89c-a11e-4c60-a480-26b17af57e95" />
