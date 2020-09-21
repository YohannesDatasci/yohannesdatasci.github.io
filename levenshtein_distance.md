---
title: Levenstein Distance
parent: Distance Measures
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>


<body>
Levenstein distance is a measure of distance between two string.<br>

Intuitive defintion is the minimum number of modifications required to obtain string b from the given string a<br>

<img src="images/levenstein_distance.jpg"><br>
The python implementation of the algorithm is the following.
</body>

```python
def edit_distance(str1,str2,m,n):
  
  if m==0:
    return n
  elif n==0:
    return m
  elif str1[m-1]==str2[n-1]:
    return edit_distance(str1,str2,m-1,n-1)
  else:
    return 1+min(

      edit_distance(str1,str2,m,n-1), # This is insert operation
      edit_distance(str1,str2,m-1,n), # this is remove opeartion
      edit_distance(str1,str2,m-1,n-1) # this is replace operation

    )
```

<body>
The logic of the algorithm is to caluclate the minimum number of , delets, and insertions, and replacements required to obtain string A from string A.
</body>