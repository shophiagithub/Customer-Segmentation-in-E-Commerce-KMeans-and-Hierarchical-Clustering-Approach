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
Calculating RFM Metrics: Recency, Frequency, and Monetary values are calculated for each customer.

python
```
r_quartiles = pd.qcut(rfm['Recency'], q=4, labels=range(4, 0, -1))
f_quartiles = pd.qcut(rfm['Frequency'], q=4, labels=range(1, 5))
m_quartiles = pd.qcut(rfm['Monetary'], q=4, labels=range(1, 5))
rfm = rfm.assign(R=r_quartiles, F=f_quartiles, M=m_quartiles)
```

