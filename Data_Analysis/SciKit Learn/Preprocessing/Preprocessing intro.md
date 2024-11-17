Consider the following data:
```csv
|x               |y               |z|
|58.0803654645808|225.699042420132|a|
|238.867356570181|247.456645333603|a|
|156.218211951778|286.588782331222|a|
```
The x and y will be our source data and we will try to predict z. We can visualize the data with this script that generates plot from the data:
```python
import numpy as np
import pandas as pd
import matplotlib.pylab as plt

df = pd.read_csv("drawndata1.csv")
X = df[['x', 'y']].values
y = df['z'] == "a"
plt.scatter(X[:,0], X[:,1], c=y)
```
![[DrawnData1CsvPlottedWithoutPreprocessing.png]]
We can notice the first problem that the x axis is on different scale then y axis. The most common way of dealing with this issue is [[Basic scaling|scaling]]. The standard way of doing scaling is with `StandardScaler` provided by Scikit-learn. This is process known as [[Standardization in Scikit-learn|standardization]]

Standardization formula: $\dfrac{x-mean(x)}{\sqrt{var}}$
When we apply the standard scaler we can see the scales in our plot chage:
```python
from sklearn.preprocessing import StandardScaler
X_new = StandardScaler().fit_transform(X)
plt.scatter(X_new[:,0], X_new[:,1], c=y)
```
![[StandardScalerOutputExample.png]]
Now we can see that the numbers are in similar scales. But we can still see that the output is not perfect, the scales are not perfectly uniform as y axis is slightly larger than x axis. Also the outliers are still present.