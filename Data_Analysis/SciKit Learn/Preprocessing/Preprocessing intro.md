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
## Using QuantileTransformer
We can remedy the outlier and uneven scaling with `StandardScaler` by using `QuantileTransofmer` from preprocessing library:
```python
from sklearn.preprocessing import QuantileTransformer
X_new = QuantileTransformer(n_quantiles=100).fit_transform(X)
plt.scatter(X_new[:,0], X_new[:,1], c=y)
```
![[QuantileTransformerExample01.png]]
The `n_quantiles` parameter is determining number of quantiles, by default it is 1000 and our data does not have that many entries. Notice that the scale is now even from 0 to 1 when using this transformer. Also the outlier clusters have lessened impact on the data and the distribution is more even when compared to `StandardScaler` used above.
### How QuantileTransformer works
Below is an example data [[Probability distribution|distribution]]. It shows some arbitrary original data and the mean is shown.
![[QuantileTransformOriginalDistribution.png]]
What we can do now is to calculate the quantiles. We can think of it as taking arbitrary points across the data and cutting the range of probability distribution. So 50% quantile([[Median|median]]) would have half of the distribution to its left and right. The 25% quantile would have 25% of the distribution to its left and 75 to its right.
![[QuantizationOfData.png]]
The QuantileTransformer then takes this data and normalizes it so the distribution is uniform or normal. For a given feature. this transformation tends to spread out the most frequent values. It also reduces the impact of marginal outliers. More information about how it effects data is [[Effects of QuantileTransformer|here]].
##