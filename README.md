# DataVine-Analytics
Summative Lab DataVine Analytics
## Findings summary for a wine classification project built for a premium wine distributor.

This project builds a wine classification system for a premium distributor, using 178 samples across 13 chemical features and 3 wine classes. The pipeline scales the data, reduces it via PCA (95% variance retained), then trains and compares three tuned classifiers.

Features were standardized before PCA to prevent high-variance features like proline from dominating, and the data was split 80/20 with stratification to preserve class balance. PCA showed that just 10 of the 13 features capture 95% of the variance, and a 2D projection revealed the three wine classes as distinct, well separated clusters , a strong sign the classes are naturally separable.

Three models were tuned and compared: 

k-Nearest Neighbors, Logistic Regression, and Random Forest. KNN and Logistic Regression stood out for combining top accuracy with low computational cost, making them the recommended choices for production. PCA reduced features are recommended for deployment to speed up inference, while the full feature set should be kept in parallel for auditing purposes. Random Forest remains a fallback option if future data becomes noisier or imbalanced.

Key limitations: 

the dataset is small (making cross-validation results somewhat optimistic), classes were balanced in training but may not be in real world batches, PCA sacrifices some interpretability, and the static dataset doesn't capture potential drift over time  so production performance should be monitored and the model retrained as needed.

## DataVine Analytics – Feed Recommendation System(chickwts.csv)

1. Business Problem

DataVine Analytics wants to recommend alternative feed types to farmers based on similar historical chicken weight performance.

We developed a recommendation system using cosine similarity to recommend the top two alternative feeds.

2. Data Preparation
Loaded the chickwts dataset.
Checked the data for missing values, duplicates, and invalid weights.
The dataset had 71 observations and 2 columns.
There were 6 feed types.
There were no missing or invalid weights.
One duplicate was removed.

4. Feed Performance Analysis

We grouped the data by feed type and calculated summary statistics including mean, median, standard deviation, minimum, and maximum weight.

Sunflower (328.92) and casein (323.58) had higher average weights, while horsebean (160.20) had a lower average.

4. PCA Analysis

PCA was used to reduce the feed performance information.

PC1 explained approximately 81.58% of the variation, meaning it captured most of the information in the feed performance profiles.

5. Cosine Similarity

Cosine similarity was used to compare feed performance patterns.

Some similarities were:

Casein , Sunflower: 0.795
Horsebean , Linseed: 0.771
Linseed , Soybean: 0.576
Casein , Meatmeal: 0.508

A score closer to 1 means greater similarity.

6. Recommendation System

The system recommends the top two alternatives for each feed:

Current Feed	Top Two Alternatives
Casein	Sunflower, Meatmeal
Horsebean	Linseed, Soybean
Linseed	Soybean, Horsebean
Meatmeal	Casein, Sunflower
Soybean	Linseed, Horsebean
Sunflower	Casein, Meatmeal

The system does not recommend the current feed itself.

7. Tuning and Evaluation

We tested top_n values of 1, 2, 3, and 4.

We selected top_n = 2 because it produced the best average similarity among the tested values and followed the lab requirement.

The system was checked to ensure that every feed received two recommendations and that recommendations were correctly ordered.

8. Business Recommendation

DataVine Analytics can use the system as a basic decision support tool when farmers are considering alternative feeds. Similarity scores should be provided so users can understand how similar the recommended feeds are.

9. Limitation

The system only considers historical chicken weight performance. It does not consider factors such as price, availability, nutrition, farm conditions, or actual performance after changing feeds.


## Regional Crime Pattern Analysis (USArrests Dataset)
## Overview

This project groups US states based on their violent crime rates using the USArrests dataset. It's Project 3 of our DataVine Analytics lab, focused on clustering and dimensionality reduction.

1. Business Problem

DataVine Analytics wants to find natural groupings among states based on crime statistics, so patterns can be used to guide decisions on where to focus resources.

2. Dataset

USArrests.csv, containing 50 states with data on Murder, Assault, UrbanPop, and Rape.

3. Approach

Loaded the data, renamed the state column, and checked for missing values and duplicates.
Selected Murder, Assault, and Rape as the most relevant features and standardized them.
Used PCA to reduce the data to 2 components.
Found the best number of clusters using the elbow method (K-Means) and BIC (GMM).
Ran K-Means and GMM clustering.
Compared the two models and visualized the results.
Results

Both methods pointed to 2 clusters as the best fit. K-Means got a silhouette score of 0.568, GMM got 0.561. The two models agreed on 49 out of 50 states (98%).

Lower crime cluster: mostly Northern and New England states like North Dakota, Wisconsin, Vermont, Minnesota, and Maine.

Higher crime cluster: mostly Southern and Western states like California, Florida, Georgia, Louisiana, and Alabama.

4. Recommendation

This grouping could help DataVine Analytics prioritize resources or interventions in higher crime regions, using the lower crime cluster as a benchmark.

5. Limitations

This only looks at three crime features from one point in time. It doesn't include things like population density, policy differences, or how crime is reported across states. Results should be treated as a general guide, not a final answer.

6. Files

Regional_Crime_Pattern_Analysis_USArrests.ipynb
USArrests.csv

7. Tools Used

Python, pandas, numpy, scikit-learn, matplotlib, seaborn

Therefore, the recommendations should be used as a guide rather than a final decision.

Final Outcome

We successfully created a basic feed recommendation engine using PCA and cosine similarity to recommend two alternative feed types based on similar historical chicken weight performance.
