---
title: Time Series Anomaly Detection
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

<body>
<h1>Predictive Difference Based Approach</h1>
The most widely used technique for time series anomaly detection is the predictive difference based approach.<br><br>

The logic of the approach is the following<br>
Step 1: Fit the predictive model to the data<br>
Step 2: Calculate the difference between the prediction and the true label, and in case the difference is too large mark the point as anomaly<br>

The problem of this approach is that it is highly depedent on predictive accuracy of the model.<br>


</body>

```python

!wget https://raw.githubusercontent.com/jbrownlee/Datasets/master/monthly-sunspots.csv
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from sklearn.preprocessing import MinMaxScaler

import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers
scaler=MinMaxScaler()

df = pd.read_csv("monthly-sunspots.csv")
df["Month"] = pd.to_datetime(df["Month"]).astype(int)// 10**11 + 69740352
# df=df.drop("Month",axis=1)
df["Month"]=scaler.fit_transform(df["Month"].values.reshape(-1,1))

model = keras.Sequential()
model.add(layers.LSTM(128,input_shape=(1,2820),activation="relu"))
model.add(layers.Dense(1))
model.compile(optimizer=tf.keras.optimizers.Adam(learning_rate=0.001),loss=tf.keras.losses.MeanSquaredError())

model.fit(x_train,y_train,epochs=10)

y_pred=model.predict(x_train)

plt.plot(x_train.reshape(2820,),y_train.reshape(2820,))
plt.plot(x_train.reshape(2820,),y_pred.reshape(2820,))
plt.show()


before_anom=abs(y_train.reshape(2820,)-y_pred.reshape(2820,))
anom_pts=np.percentile(before_anom,95)
anoms=np.where(before_anom>anom_pts,1,0)
```

<body>
Another well known approach for time series anomaly detection is treating time-series as a collection of datapoints utilizing any anomaly detection algorithm to obtain the anomalies.</br>
</body>

```python
!wget https://raw.githubusercontent.com/jbrownlee/Datasets/master/monthly-sunspots.csv
from sklearn.ensemble import IsolationForest
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("monthly-sunspots.csv")

anomaly=IsolationForest(n_estimators=100,contamination=0.05).fit_predict(df["Sunspots"].values.reshape(-1,1))

plt.plot(df.index,df.Sunspots)
for i,j in enumerate(anomaly):
  if j == -1:
    plt.plot(df.index.values[i],df.Sunspots.values[i],"g*")

plt.show()
```

<body>
Anomaly detection using the confidence intervals is another well known technique for obtaining the anomalies in time series data.<br>
</body>

```python
!wget https://raw.githubusercontent.com/jbrownlee/Datasets/master/monthly-sunspots.csv
from fbprophet import Prophet
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("monthly-sunspots.csv")
df=df.rename(columns={"Month":"ds","Sunspots":"y"})

prop = Prophet()
prop.fit(df)
pred=prop.predict(df)

anom_pred=np.where(df.y<=pred.yhat_upper,np.where(df.y>=pred.yhat_lower,1,-1),-1)

plt.plot(df.index,df.y)
for i,j in enumerate(anom_pred):
  if j == -1:
    plt.plot(df.index.values[i],df.y.values[i],"g*")

plt.show()
```
<body>
Lesser known technique for anomaly detection is to use connectivity based clustering algorithms for anomaly detection.
</body>
```python
!wget https://raw.githubusercontent.com/jbrownlee/Datasets/master/monthly-sunspots.csv
from sklearn.cluster import DBSCAN
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df=pd.read_csv("monthly-sunspots.csv")

dbscan=DBSCAN(eps=0.5,min_samples=10)
dbscan_out=dbscan.fit_predict(df.Sunspots.values.reshape(-1,1))

plt.plot(df.index,df.Sunspots)
for i,j in enumerate(dbscan_out):
  if j == -1:
    plt.plot(df.index.values[i],df.Sunspots.values[i],"g*")

plt.show()
```