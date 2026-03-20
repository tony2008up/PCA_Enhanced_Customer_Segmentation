# PCA-Enhanced Customer Segmentation for Credit Card Marketing

## Project Overview
This project applies **Principal Component Analysis (PCA)** and **clustering techniques** to segment credit card customers for marketing purposes.  
The goal is to reduce feature redundancy, improve cluster quality, and identify meaningful customer groups that can support targeted business strategies.

The notebook walks through the full workflow:
- data loading and inspection
- data cleaning
- exploratory data analysis
- feature scaling
- PCA for dimensionality reduction
- clustering model comparison
- customer segment profiling
- marketing recommendations

## Dataset
The dataset contains **8,950 customer records** and **18 columns**:
- **1 ID column**: `CUST_ID`
- **17 behavioral / financial features**, such as:
  - `BALANCE`
  - `PURCHASES`
  - `ONEOFF_PURCHASES`
  - `INSTALLMENTS_PURCHASES`
  - `CASH_ADVANCE`
  - `CREDIT_LIMIT`
  - `PAYMENTS`
  - `TENURE`

`CUST_ID` is used only as a unique identifier and is removed before modeling.

## Data Cleaning
The notebook checks:
- data types
- missing values
- duplicate rows

### Cleaning Summary
- **8,950 rows**
- **18 columns**
- no major data quality issues after inspection
- missing values were removed or handled
- duplicate rows were checked
- numeric features were prepared for clustering

This produces a clean dataset ready for scaling and dimensionality reduction.

## Exploratory Data Analysis
EDA includes:
- summary statistics
- correlation heatmap
- pairplot

### Main Findings
- purchase-related variables are strongly positively correlated
- cash advance variables are also closely related
- several features contain overlapping information
- the dataset is suitable for **PCA** because of multicollinearity among features

These patterns suggest that dimensionality reduction can simplify the feature space without losing much information.

## Feature Scaling
Before PCA and clustering, all numerical features are normalized using **MinMaxScaler**.

Why scaling matters:
- clustering algorithms are distance-based
- financial variables have very different ranges
- scaling prevents large-value variables from dominating the clustering process

After scaling, all features are transformed into the range **[0, 1]**.

## PCA Dimensionality Reduction
PCA is applied to the scaled dataset to reduce the original **17 features** into a smaller number of components while preserving most of the information.

### PCA Results
- **PC1 explains 49.6%** of total variance
- first **3 components explain 76.5%**
- first **5 components explain 91.1%**
- first **7 components explain 96.54%**

Using `n_components=0.95`, PCA automatically selects:

- **7 principal components**

This reduces model complexity while retaining at least **95% of the variance**.

## Clustering Models Compared
The notebook compares several clustering approaches on the PCA-transformed dataset:

### K-Means
- KMeans with `k = 3, 4, 5, 6`

### Hierarchical Clustering
- Agglomerative clustering with different linkage methods:
  - ward
  - average
  - complete

### DBSCAN
- multiple combinations of `eps` and `min_samples`

## Model Evaluation
The clustering models are evaluated mainly with the **silhouette score**.

### Best Result
The best-performing model is:

- **KMeans (k = 3)**
- **Silhouette Score: 0.3837**

### Improvement Over Previous Assignment
The notebook compares this result with the earlier clustering assignment:

- previous best score: **0.2546**
- current best score: **0.3837**
- improvement: **+0.1291**

This shows that applying PCA before clustering improved cluster separation and cohesion.

## Visualization
The notebook includes:
- explained variance table
- PCA scatter plot (`PC1` vs `PC2`)
- cluster size histogram

### Cluster Distribution
For the final **KMeans (k=3)** model:
- **Cluster 0**: 4,728 customers (~52.8%)
- **Cluster 1**: 2,786 customers (~31.1%)
- **Cluster 2**: 1,436 customers (~16.0%)

The PCA scatter plot shows visible separation between the three customer groups.

## Customer Segments
The final clusters are interpreted using the original, non-PCA data.

### Cluster 0 – Low Activity / Basic Users
- largest group
- relatively low purchases
- moderate to high revolving usage
- lower full-payment rate

**Possible strategy:** encourage more card usage through cashback offers, small spending rewards, or activation campaigns.

### Cluster 1 – Active Purchasers / Valuable Customers
- stronger purchase activity
- more regular card usage
- healthier payment behavior

**Possible strategy:** retain with loyalty programs, premium benefits, and personalized offers.

### Cluster 2 – High Credit / Premium Customers
- smaller but more valuable segment
- higher balances, spending, or credit limits
- important for premium marketing strategy

**Possible strategy:** focus on premium cards, travel rewards, exclusive promotions, and relationship management.

## Business Value
This project demonstrates how unsupervised learning can support business decision-making by:
- identifying distinct customer groups
- improving campaign targeting
- supporting retention strategies
- reducing waste in broad marketing campaigns
- helping financial institutions personalize product recommendations

## Technologies Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn

## How to Run
1. Clone the repository.
2. Install required libraries:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```
3. Open the notebook:
   ```bash
   jupyter notebook PCA_Enhanced_Customer_Segmentation.ipynb
   ```
4. Run all cells in order.

## Repository Structure
```bash
.
├── PCA_Enhanced_Customer_Segmentation.ipynb
├── README.md
└── dataset files
```

## Key Takeaways
- PCA successfully reduced the feature space from **17 variables to 7 principal components**
- the reduced space still retained **over 95% of the variance**
- clustering performance improved noticeably after PCA
- **KMeans (k=3)** produced the best segmentation result
- the final clusters can be translated into practical marketing actions

## Future Improvements
Possible next steps:
- test other dimensionality reduction methods such as t-SNE or UMAP for visualization
- try Gaussian Mixture Models or other clustering methods
- perform deeper feature engineering
- validate business usefulness with real marketing response data
- add dashboard-style visual summaries for stakeholders

## Acknowledgment
This project was completed as part of a machine learning / customer segmentation assignment focused on combining **PCA** with **unsupervised clustering** for marketing analysis.
