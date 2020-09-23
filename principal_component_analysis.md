---
title: Principal Component Analysis
parent: Anomaly  Detection
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

<body>
<img src="images/pca_pseudocode.png">
Principal component analysis (PCA) is the process of computing the principal components and using them to perform a change of basis on the data, sometimes using only the first few principal components and ignoring the rest.<br>

The logic behind the algorithm is to approximate the current data with lower dimensional principal component representation<br>
<bold>Step 1:<bold> Calculate the convariance or correlation matrix with the corresponding eigenvectors and eigenvalues<br>
<bold>Step 2:<bold> Sort eigenvectors based on their eigenvalues and in case of dimenisonality reduction drop some of them<br>
<bold>Step 3:<bold> Approximate the dataset by the product of the eingenvectors and the original dataset<br>

Now here comes an intuitive question how can PCA be used for anomaly detection<br>

The PCC(principal component classifier) has been first described by Ling et al. in the <a href="http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.66.299&rep=rep1&type=pdf">paper</a><br>

let us denote yi is the ith principal component of that is equal to ei(x-mean) where ei is the ith eigenvector.<br>
<img src="images/pca_xattack.png"><br>
Otherwise classify the instance as an anomayl.<br>
The intuition for the formula is following. The formula gives approximation of mahalanobis distance between the point and principal components. Thus the first sum is the distance between the point and the chosen K principal components which shows whether the given point conforms to the structure of the data. The second sum is the distance between the point and the not chosen n-K components which shows how close the given point which helps to detect the extreme value anomalies.<br>

</body>