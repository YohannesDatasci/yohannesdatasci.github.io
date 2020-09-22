---
title: DBSCAN
parent: Clustering
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

<body>

<img src="images/pseudocode-of-the-DBSCAN-algorithm.png"><br>


the logic behind the algorithm is the following<br>

The input parameters are, epsilon, minpts and distance_measure<br>

Step 1: pick a random unvisited point p from the input data<br>
Step 2: Check if there are at least minpts number of points in the epsilon  neighborhood of p<br>
Step 3: If not, then mark p as noise else ExpandCluster(p)<br>

The ExpandCluster functon has the following logic<br>

Step 1: add point p to cluster c<br>
Step 2: iterate over all neighouring points of p<br>
Step 3: for each neighbouring point check if there are at least minpts number of points in epsilon neighborhood<br>
Step 4: If yes, then add the neighbouring points of the p' to the neighbouring points of p<br>
Step 4: add neighbouring points to the cluster c<br>

The advantages of DBSCAN is its speed, ability to capture robust shapes of clusters, robustness to outliers<br><br>

The disadvatnage of DBSCAN is the inability to cluster datasets with varying density<br>

To address these issues the following algorithms have been developed<br>

<img src="images/optics_pseudocode.png"><br>
OPTICS is an algorithm that tries to solve this issue<br>
It introduces two new cocncepts the core-distance and reachability<br>

core-distance is the minimum epsilon for which the given core will include minpts number of points<br>
reachability is the max between euclidean distance to the point q and core-distance for give the point p.<br>

It is important to note that OPTICS by itself is not a clustering algorithm, however, it produces a reachability plot which could be used to sperate the clusters in the data.<br>
The logic of algorithm is to process the points with priority based on their reachability distance, which uncovers hidden structures in the data and allows to cluster them.

OPTICS itself is not a clustering algoirthm, but it can be converted to so by selecting a treshold value for the hierarchical reachability structure.<br>

The weakness of OPTICS is that it is too computationaly heavy and does not scale for big data.<br>

The HDBSCAN came to rescue this situation<br>

<img src="images/hdbscan_pseudocode.png">

TODO:// explain HDBSCAN

</body>