# Restaurant-Datascience

PROJECT BASED UPON USING REST API TO EXTRACT DATA ABOUT RESTAURANTS IN AREA AND FINDING THE BEST ONE FOR YOU THROUGH CLUSTERING ALGORITHM.RESTAURANTS ARE PLOTTED IN AREA USING PLOTLY FOR BETTER VISUALS.HERE IS AN EXAMPLE OF ME LOOKING FOR CHINESE FOOD NEAR ME

![newplot](https://user-images.githubusercontent.com/20189314/188161192-29b0e4ff-b8bd-40e6-a022-aeb4030e6b1f.png)

**GOAL**
Provide users a recommendation system with an unsupervised live-time algorithm based on distance,rating and reviews.

**DATA**
The Yelp Developers platform provided the restaurant api and the reviews api(for future use).The requests library was used to make Api calls for the user which returned the dataset in JSON format.
Requires User location and api alongside food preference to start with.

**Cleaning and Feature Engineering**
Extracted information from JSON format to mine the categories and coordinates column in the dataframe
Converted the price which was returned with the symbol ($) to a number for the model.Since the value actually is not purely categorical and a higher integer actually means a higher price,this change was made.
Distance was converted to its absolute value
Imputed missing prices with the average of the category it belonged to,

**MODEL**
Used the K-means algorithm:Minimize euclidean distance between points and cluster centroids.
The data used only contained the ratings,distance and prices.
The distances were on a much larger scale to the the other data so the standard scaler was used to convert the data to N(0,1) distribution
Why use KMEANS?
  -Unsupervised-Since the data I used was from an api and got it livetime,we needed an algorithm which did not need to be trained and could work on the spot.
  -Linear-time complexity-Since our code works live-time,we need the fastest algorithm and the linear time complexity makes it a very good choice.
  -Easy Visualization-The cluster centroids and points can easily be visualized using scatterplots to assess their performance.

**METRICS**
Worked strictly with Inertia to measure distance of points within Cluster(Sum of squared distances of samples to their closest cluster center, weighted by the sample weights if provided).
The intracluster distances are summed up.
In my findings,the most common number of clusters found by using the elbow plot with the intertia and cluster numbers was 3.This gave us the lowest steep down on inertia.

**Findings**
We found that our model clustered the data into 3 sets of price vs distance :LOW DISTANCE-MID PRICE, LARGE DISTANCE-MID PRICE, HIGH PRICE-LOW DISTANCE.When the ratings were used as a label for this plot,we could find the restaurants which would be perfect for users to visit namely the Low distance-Mid price restaurants with high review ratings.
Issues:
K-means does not deal well with outliers in our dataset and moves the cluster out too much.This was seen with large distances
It also does not do well with clusters of different shapes and sizes which was present in our findings.

**Future Improvements**
Use a new method in DBSCAN (Density-Based Spatial Clustering of Applications with Noise): This algorithm is particularly effective for identifying clusters of arbitrary shapes. It works well with spatial data and is robust against outliers.
Use a sentiment analysis model to provide a review score for the restaurant based on reviews given.This would be useful since there are comments which do not rate appropriately to the review they provided.This can be due to prejudgement bias.This method was tried with a voting classifiers but unfortunately,the API only gives us 3 comments which is not enough to judge and review a restaurant correctly.With a higher number of comments,this can be done better.
Rest of the code on GOOGLE COLAB DOC
