# Customer-Segmentation-in-E-Commerce-KMeans-and-Hierarchical-Clustering-Approach

![simplistic-man-and-woman-discussing-project](https://github.com/shophiagithub/Customer-Segmentation-in-E-Commerce-KMeans-and-Hierarchical-Clustering-Approach/assets/114874837/017bc047-9095-40bf-a7c7-f81aaeac66b5)

## Table of Contents
- [Introduction](#Introduction)
- [Project Overview](#Project_Overview)
- [Data](#Data)
- [RFM Analysis](#RFM_analysis)
- [Modeling](#Modelling)
- [Evaluation](#Evaluation)
- [Conclusion](#Conclusion)
- [Tools Used](#Tools_used)

## Introduction

Customer segmentation is essential for e-commerce businesses to understand their customer base and tailor marketing strategies accordingly. This project leverages KMeans and Hierarchical (Agglomerative) Clustering techniques, along with RFM (Recency, Frequency, Monetary) and cohort analysis, to segment customers and identify VIP clients.

## Project Overview

1. **Data Collection**: The project utilizes historical transaction data from an e-commerce dataset.
2. **Preprocessing**: The data is processed to calculate total spending per transaction and relevant RFM metrics.
3. **Modeling**: KMeans and Hierarchical Clustering models are applied to the preprocessed data.
4. **Evaluation**: The models' performances are evaluated using visualizations and statistical metrics.
5. **VIP Client Identification**: VIP clients are identified based on their RFM scores and clustering results.

## Data

The dataset contains transaction records, including the following columns:

- InvoiceNo
- StockCode
- Description
- Quantity
- InvoiceDate
- UnitPrice
- CustomerID
- Country

## RFM Analysis
1. Calculating RFM Metrics: (`Recency`,`Frequency`,`Monetary` )values are calculated for each customer.

```python
r_quartiles = pd.qcut(rfm['Recency'], q=4, labels=range(4, 0, -1))
f_quartiles = pd.qcut(rfm['Frequency'], q=4, labels=range(1, 5))
m_quartiles = pd.qcut(rfm['Monetary'], q=4, labels=range(1, 5))
rfm = rfm.assign(R=r_quartiles, F=f_quartiles, M=m_quartiles)
```
2. Creating RFM Segments: RFM segments are created by combining the (`R`, `F`, and `M`) scores.

```python
def add_rfm(x): return str(x['R']) + str(x['F']) + str(x['M'])
rfm['RFM_segment'] = rfm.apply(add_rfm, axis=1)
rfm['RFM_score'] = rfm[['R', 'F', 'M']].sum(axis=1)
```

## Modeling
## KMeans Clustering
Determination of optimal number of clusters using the Elbow Method:
```python
from sklearn.cluster import KMeans
from yellowbrick.cluster import KElbowVisualizer

print('Elbow Method to determine the number of clusters to be formed')
Elbow_m = KElbowVisualizer(KMeans(), k=10)
Elbow_m.fit(rfm_normalized)
Elbow_m.show()
```
![image](https://github.com/shophiagithub/Customer-Segmentation-in-E-Commerce-KMeans-and-Hierarchical-Clustering-Approach/assets/114874837/cabfb46c-83ce-402b-bbb1-eab5b4fc10bb)


## Hierarchical Clustering
## Visualization of the Dendrogram:
```python
from scipy.cluster.hierarchy import dendrogram, linkage
plt.figure(figsize=(17, 8))
dendo = dendrogram(linkage(rfm_normalized_ac, method='ward'))
plt.title('Dendrogram', fontsize=15)
plt.show()
```
![image](https://github.com/shophiagithub/Customer-Segmentation-in-E-Commerce-KMeans-and-Hierarchical-Clustering-Approach/assets/114874837/cf943529-7d1e-4cac-9a2e-9a12e1e835e7)

![image](https://github.com/shophiagithub/Customer-Segmentation-in-E-Commerce-KMeans-and-Hierarchical-Clustering-Approach/assets/114874837/36ed5264-e116-4cd9-8fe5-c4c116f7ee6c)


## Evaluation
The clustering results are evaluated through visualizations and the identification of VIP clients based on their RFM scores and clustering labels.

## VIP Clients Segmentation
Identification of VIP clients:
```python
rfm_vip = rfm[(rfm["cluster_labels"] == 1) & (rfm["Frequency"] >= rfm["Frequency"].quantile(0.95)) & (rfm["Monetary"] >= rfm["Monetary"].quantile(0.95)) & (rfm["Recency"] <= rfm["Recency"].quantile(0.30))]
VIP_clients = rfm_vip[["Recency", "Frequency", "Monetary"]]
```

## Conclusion
The project successfully demonstrates the application of KMeans and Hierarchical Clustering in customer segmentation for e-commerce. The use of RFM and cohort analysis provides additional insights into customer behavior, and the identification of VIP clients can help tailor marketing strategies.

## Tools Used
1. **Python**: Programming language used for the project.
2. **Pandas**: Library for data manipulation and analysis.
3. **NumPy**: Library for numerical computations.
4. **Scikit-learn**: Library for machine learning algorithms and utilities.
5. **Matplotlib**: Library for creating static visualizations.
6. **Seaborn**: Library for statistical data visualization.
