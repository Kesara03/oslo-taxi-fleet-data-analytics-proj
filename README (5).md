# Customer Segmentation with K-Means Clustering

A machine learning pipeline for customer segmentation using K-Means clustering, deployed as an interactive Streamlit application for real-time segment prediction.

## Overview

This project implements unsupervised learning to identify natural customer groups based on demographic and behavioral attributes. The trained model segments customers into distinct profiles that enable targeted marketing strategies, personalized communications, and optimized budget allocation.

## Technical Architecture

```
Raw Data --> Preprocessing --> K-Means Clustering --> Model Serialization --> Streamlit App
   |              |                   |                      |                    |
 CSV File    Encoding &          Elbow Method           pickle export      Real-time
             Feature Prep        + Fit/Predict                             Predictions
```

## Dataset

Source: [Mall Customer Segmentation Data (Kaggle)](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python)

| Feature | Description |
|---------|-------------|
| Gender | Male/Female (encoded as 1/0) |
| Age | Customer age in years |
| Annual Income (k$) | Yearly income in thousands USD |
| Spending Score (1-100) | Mall-assigned score based on purchasing behavior |

## Methodology

### 1. Data Preprocessing
- Binary encoding for categorical gender variable
- Feature selection excluding CustomerID (non-predictive identifier)

### 2. Optimal Cluster Selection
The Elbow Method was applied across k = 1 to 9 clusters, plotting Sum of Squared Errors (SSE) against cluster count. The inflection point at k = 3 indicated optimal segmentation.

### 3. Model Training
```python
kmeans = KMeans(n_clusters=3, random_state=42)
df['cluster'] = kmeans.fit_predict(df)
```

### 4. Cluster Validation
Silhouette Score: **0.34** (measures intra-cluster cohesion vs. inter-cluster separation)

## Customer Segments

| Cluster | Segment Profile | Characteristics |
|---------|-----------------|-----------------|
| 0 | Low Income - Low Spending | Conservative spenders with limited income |
| 1 | High Income - High Spending | Premium customers with high purchasing power |
| 2 | Young Low Income - High Spending | Younger demographic with high engagement despite lower income |

## Project Structure

```
.
├── customer_clustering_kmeans.ipynb  # Model development notebook
├── app.py                            # Streamlit application
├── kmeans.pkl                        # Serialized trained model
├── Mall_Customer_Segmentation_Data.csv
└── README.md
```

## Deployment

The trained K-Means model is serialized using pickle and integrated into a Streamlit application. Users input customer attributes through the UI and receive real-time segment predictions.

### Running the Application

```bash
pip install streamlit pandas numpy scikit-learn
streamlit run app.py
```

### Input Parameters
- Gender (Male/Female)
- Age (18-70)
- Annual Income (10-150 k$)
- Spending Score (1-100)

## Dependencies

| Package | Purpose |
|---------|---------|
| pandas | Data manipulation |
| numpy | Numerical operations |
| scikit-learn | K-Means clustering, silhouette scoring |
| matplotlib | Elbow curve visualization |
| streamlit | Web application framework |
| pickle | Model serialization |

## Results

The segmentation enables actionable business insights:
- **Cluster 0**: Budget-conscious promotions, value-focused messaging
- **Cluster 1**: Premium offerings, loyalty programs, exclusive access
- **Cluster 2**: Trend-driven campaigns, payment flexibility options

## Author

Kesara Rathnasiri
