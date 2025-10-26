# SUMMARY
## MODEL - 1
Clusters found: 3 (based on elbow method).
Only 2 PC's taken for they contribute the maximum variation in this dataset
Cluster characteristics:  
Cluster 1 → Big/powerful Pokémon (high PC1: height/weight/attack)  
Cluster 2 → Small/weaker Pokémon (low PC1)  
Cluster 3 → Fast Pokémon (high PC2: speed)  

PC1 (height/weight/attack) separates big vs small Pokémon.  
PC2 (speed) separates fast vs slow Pokémon.  
K-Means clusters align well with this 2D PCA visualization.  
DBSCAN clusters may identify the same groups but also label rare Pokémon as noise.  

K-Means is more suitable because the clusters are mostly spherical in the normalized 8D stats space, we have a clear idea of 3 clusters, and we want interpretable centroids.  
DBSCAN is useful if we expect irregular clusters or want to identify outlier Pokémon, but here it has only grouped the data into 1 and -1 (for outlier pokemon's) so it is not useful.


## MODEL - 2
Best Random Forest F1-score: 0.647, AUC: 0.997  
Optimal Parameters → Depth: 10.0, Trees: 10.0  
Most Important Feature → oldbalanceOrg  

High Recall is critical for fraud detection (better to catch more frauds, even if precision drops slightly).  

The model is overfit because of the limitations of my laptop, here we have only taken 100,000 rows out of nearly 6 million, and so the model isn't giving result as expected.
