---
title: Isolation Forest
parent: Anomaly  Detection
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>


<body>


The original source of the algorithm is the paper by Liu et al. https://ieeexplore.ieee.org/document/4781136<br>

<img src="images/isolation_forest_trees.png"><br>

The algorithm defining the forest of isolation trees has the following steps.<br>
<br><br>
<bold>Step 1:</bold> Define height limit as $$ceiling(\log_2^\phi)$$<br>
<bold>Step 2:</bold> At each iteration take a random sample from the input dataset to train a single isolation Tree:<br>
<bold>Step 3:</bold> Train a single isolation tree on the random sample<br>
<bold>Step 4:</bold> return average path length for a single datapoint<br>
Now let us discuss how each individual tree is built.

<img src="images/isolation_forest_pseudocode.png"><br>

<bold>Step 1:</bold> randomly select an attribute q from the provided input data<br>
<bold>Step 2:</bold> randomly select a split point p from min to max of the attribute q<br>
<bold>Step 3:</bold> If only single datapoint is left return <br>
<bold>Step 3:</bold> repeat steps 2 and 3 untill all the datapoints are separated by the tree<br>

An intuitive question might arise. How do one evaluate the model on test data after training the isolation forest.<br>

<img src="images/isolation_forest_pathlen.png"><br>

<bold>Step 1:</bold> iterate over all datapoints in the given evaluation input<br>
<bold>Step 2:</bold> For each datapoint calculate the Pathlength of the single datapoint by calculating number of edges from the root node to the terminating node containing the datapoing<br>

Here an important remarks is that if the datapoint terminates at external node with the size>1 then the c(Size) therm is added to the path lenght as a row estimation for the missing edges to the terminating node. The formula of c is the following.<br>

<img src="images/isolationcn.png"><br>

</body>