To visualize how the QuantileTransformer works, we can look data from StandardScaler. To do this we can use following code:
```python
import numpy as np
import pandas as pd
import matplotlib.pylab as plt
from sklearn.preprocessing import StandardScaler, QuantileTransformer
from sklearn.neighbors import KNeighborsClassifier
from sklearn.pipeline import Pipeline 

df = pd.read_csv("../Data/drawndata1.csv")
X = df[['x', 'y']].values
y = df['z'] == "a"

def plot_output(scaler):
    pipe = Pipeline([
        ("scale", scaler),
        ("model", KNeighborsClassifier(n_neighbors=20, weights='distance'))
    ])

    pred = pipe.fit(X, y).predict(X)

    plt.figure(figsize=(9, 3))
    plt.subplot(131)
    plt.scatter(X[:, 0], X[:, 1], c=y)
    plt.title("Original Data")
    plt.subplot(132)
    X_tfm = scaler.transform(X)
    plt.scatter(X_tfm[:, 0], X_tfm[:, 1], c=y)
    plt.title("Transformed Data")
    plt.subplot(133)
    X_new = np.concatenate([
        np.random.uniform(0, X[:, 0].max(), (5000, 1)), 
        np.random.uniform(0, X[:, 1].max(), (5000, 1))
    ], axis=1)
    y_proba = pipe.predict_proba(X_new)
    plt.scatter(X_new[:, 0], X_new[:, 1], c=y_proba[:, 1], alpha=0.7)
    plt.title("Predicted Data")
plot_output(scaler=StandardScaler())
```
![[StandardScalerTransformExample.png]]
As we cam see from the predicted data, the outliers create zones that would classify as yellow. But from the data we can see that this is not that accurate classification. If we call the `plot_output` with QuantileTransformer:
```python
plot_output(scaler=QuantileTransformer(n_quantiles=100))
```
![[QuantileTransformerEffectExample.png]]
As we can see, the data is distributed more evenly. The predictions better match the output.
>[!warning]
>The data is being trained on the same data that the predictions are made for. In practice we need to divide the data to training and predicting datasets.

