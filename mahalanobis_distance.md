---
title: Mahalanobis Distance
parent: Distance Measures
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>


<body>
$$D_{M}({\vec {x}})={\sqrt {({\vec {x}}-{\vec {\mu }})^{T}S^{-1}({\vec {x}}-{\vec {\mu }})}}$$


The mahalanobis distance is the distance between a point and a distribution in multivariate space, and not between two points.<br>


The intition behind the mahalanobis distance is that simply computing the euclidean distance between the centroid of distribution and the point is not reliable as the distribution can have a high variance, this can be overcome by measuring how many standart deviations away is the given point to the distribution however, that is biased as well because we assume that standart deviation is uniform in the distribution and it has a spehrical form. The overcome this limiations, mahalanobis distance was introduced<br>
</body>