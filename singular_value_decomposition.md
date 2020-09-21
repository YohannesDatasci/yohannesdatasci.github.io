---
title: Singular Value decomposition
parent: Linear Algebra
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

<body>
Singular value decompostion is a technique of factoring the given matrix into the product of three lower dimensional vectors.<br>
<img src="images/svd_image.jpeg"><br>
U and V matrices are the eigenvectors of $$AA^T$$ and $$A^TA$$, and the S matrix is the diagonal matrix of positive eigenvalues of these two matrices.
</body>
```python
import numpy as np
from scipy.linalg import svd
test_matrix=[[1,2,3],[4,5,6],[7,8,9]]
u,s,vt = svd(test_matrix)
s=np.diag(s)
print(u.dot(s.dot(vt)))
```