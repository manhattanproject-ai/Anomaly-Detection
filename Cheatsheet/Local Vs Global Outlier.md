# Local Vs Global Outlier 

The difference between Local and Global Outliers is dependent on the context of the surrounding data points. While a Global Outlier is an extreme anomaly when compared to the entire dataset, a Local Outlier is only an anomaly when compared to its immediate neighborhood or
cluster.

This distinction is crucial for anomaly detection techniques like LOF (Local Outlier Factor), which is designed to spot local differences.

## Global Outlier (Absolute Anomaly) 🌍
A Global Outlier is a data point that deviates significantly from all other data points in the entire dataset. It is an absolute extreme that stands out regardless of the specific cluster it's near.

### Detailed E-commerce Example: Order Value
* Dataset: All customer orders over the last year.
* Normal Behavior: 99.9% of orders fall between $10 and $500.
* Anomaly: A single order for $50,000.
* Reasoning: This value is so far removed from the bulk of all other order values that it is considered a Global Outlier. It doesn't matter if the customer usually buys luxury goods or budget items; a $50,000 order is globally anomalous and signals a high-priority event 
(e.g., massive fraud, or a legitimate but extremely rare corporate purchase).

## Local Outlier (Contextual Anomaly) 🏘️
A Local Outlier is a data point that is an anomaly relative to the data points in its specific local cluster or neighborhood, even though it might not be a major outlier when compared to the entire dataset.

### Detailed E-commerce Example: Customer Shipping Frequency
* Dataset: Customer order frequency (orders per month) and average order value.
* Cluster 1 (Casual Shoppers): Customers who place 1-2 orders/month with an average value of $50. (Low Frequency, Low Value).
* Cluster 2 (Bulk Buyers): Customers who place 1-2 orders/month with an average value of $1,000. (Low Frequency, High Value).
* Anomaly: A customer in the Casual Shoppers (Cluster 1) group suddenly places 10 orders in one month, but all with a low average value of $50.
* Reasoning:
  * Not a Global Outlier: Other customers in the Bulk Buyers group routinely have high monthly order counts (e.g., 10-15 orders), so an order count of 10 is not globally extreme.
  * Is a Local Outlier: When compared only to their direct neighbors in the Casual Shoppers cluster (who average 1-2 orders/month), this customer's behavior (10 orders) is highly unusual.
* Implication: This local deviation suggests a possible change in behavior (e.g., the customer became a dropshipper, or their account was taken over by someone testing small orders) that would be missed by simply checking the overall average.

## Visual Comparison

<img width="956" height="593" alt="image" src="https://github.com/user-attachments/assets/a6a3d792-a692-4a01-9755-8e7cf2609b90" />

As seen in the image, the points labeled Global Outliers are far away from all clusters, while the points labeled Local Outlier for Cluster C1 are close to the main data points of the overall population but are clearly outside the tightly packed boundary of their 
local cluster.
