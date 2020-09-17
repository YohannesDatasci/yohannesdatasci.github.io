---
title: KMeans
parent: Clustering
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>


<body>
<img src="images/kmeans.png">
The logic behind the standard kmeans is the Lloyd's algorithm the steps of which are as follows.<br>
Step 1 is to randomly initialize k distinct datapoints as centriods.<br>
Step 2 iterate over each datapoint and assign them to the cluster with the centroid that has nearest euclidean distance to the point.<br>
Step 3 update the centroids by setting them equal to the mean of all points in the relative cluster.<br>

However, due to random initialization of the first centroids the k-means algorithm does not necessarily converge to optimal results.<br>
In order to decrease the sensitivity of the k-means algorithm to random initialization, multiple techniques have been developed.<br>
<img src="images/poor_init.png">

In general, the random initialization of kmeans would result in poor clustering similar to the image above <br>

The most well known method to solve the problem is to run the algorithm n-times and choose the best resulting clusters, by comparing <br>the variance inside each cluster. It is assumed that the lesser variance clusters have the better is the actual clustering result.<br>

Second known technique to solve this problem is k-means++. The only difference between k-means++ and standart kmeans is the specially <br>crafted initialization phase. The steps of k-means++ initialization algorithm are as follows.<br>

Step 1 pick a random datapoint as our first centroid<br>
Step 2 for each point computer distance between the point and the nearest centroid<br>
Step 3 randomly select a new centroid with weighted probability distributions where each point has a probability proportion of D(x)^2 to be chosen<br>
Step 4 repeat steps 2 and 3 untill the k centroids are already chosen.<br>
After these steps are over, standart kmeans algorithm is utilized to obtain a convergent clustering.<br>

<img src="images/good_init.png">

The kmeans++ initialization would generally result in better clustering like in the image above.<br>

However, this is not the last flaw of the kmeans algorithms. Kmeans also suffers from distance metric inflexibility, meaning that the measure of distance cannot be arbitrary similarity measuer. Secondly kmeans is not robust to outliers as it utilizes mean to obtain the centroids.<br>

To resolve the problem another algorithm was introduced to the game, and k-medioids is its name.<br>

As the algorithm uses medians to calculate the medioids it is more robust to the outliers, also due to the algorithm using dissimilarity measure to estimate the medioids, it is not dependant on distance based measures thus it could be arbitrary dissimilarity measure.<br>

The steps of the algorithm are as follows.<br>
Step 1 kmeans++ initialization<br>
Step 2 associate each datapoint to the closest medioid<br>
Step 3 For each element in cluster, make the element the new centroid, associate each datapoint to the closest medioid and compute the cost.<br>
Step 4 if cost decreased then repeat 2 and 3 else finish.<br>

As you can see the main flaw of the k-medioids algorithm is that it's time complexity is beyond evil, also the k-medioids fails to cluster non-spehrical data points as it uses compactness as clustering criteria not connectivity.<br>
</body>
