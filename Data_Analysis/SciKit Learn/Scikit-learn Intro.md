# Data and model
Consider the following example:
```python
import sklearn
from sklearn.datasets import fetch_california_housing
X, y = fetch_california_housing(return_X_y=True)
#output:
(array([[   8.3252    ,   41.        ,    6.98412698, ...,    2.55555556,
           37.88      , -122.23      ],
        [   8.3014    ,   21.        ,    6.23813708, ...,    2.10984183,
           37.86      , -122.22      ],
        [   7.2574    ,   52.        ,    8.28813559, ...,    2.80225989,
           37.85      , -122.24      ],
        ...,
        [   1.7       ,   17.        ,    5.20554273, ...,    2.3256351 ,
           39.43      , -121.22      ],
        [   1.8672    ,   18.        ,    5.32951289, ...,    2.12320917,
           39.43      , -121.32      ],
        [   2.3886    ,   16.        ,    5.25471698, ...,    2.61698113,
           39.37      , -121.24      ]]),
 array([4.526, 3.585, 3.521, ..., 0.923, 0.847, 0.894]))
```
This code represents data of housing prices in California. The data is separated into two objects: X and y. X represents various data about the houses and y represents cost of the houses in thousands of dollars. This data is then passed onto a the Scikit-learn model and it trains on that data. The trained model then can make predictions.
![[ScikitLearnModelExample.png]]
X = data about houses per district, y = house prices per district in units of 100,000 USD

In Scikit the there two steps in making a model. First we create the model python object and then we train it on data. The training is done via `.fit(X, y)` function.
## The models
Scikit provides many models. Lets start with [[KNeighborsRegressor|nearest neighbor regressor]]. Here is example of how such model can be prepared and visualized with scatter graph on the predicted values against the original:
```python
from sklearn.neighbors import KNeighborsRegressor
import matplotlib.pylab as plt
mod = KNeighborsRegressor()
mod.fit(X, y)
pred = mod.predict(X)
plt.scatter(pred, y)
```
![[ScikitIntroScatterPlot.png]]
On x axis is predicted values, on y xis is trained values
> [!info] California dataset
> The data is capped at 5, values above were truncated

There is small problem with this approach however. As we can see from the data, it is quite noisy. Scikit learn provides way of [[Basic scaling|scaling]] the data appropriately. With the scaling provided we can think of the model as set of multiple operations:
![[ExpandedModelExample.png]]
## The pipelines and models
When we need to properly scale the model, we can use [[Pipelines|pipelines]]. When we create such pipelines we can treat it as complete model and perform `.fit(X,y)` and `.predict` operations on them. Here is an example of our python script with pipeline and scaling:
```python
import sklearn
from sklearn.datasets import fetch_california_housing
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsRegressor
import matplotlib.pylab as plt

X, y = fetch_california_housing(return_X_y=True)

pipe = Pipeline([
	("scale", StandardScaler()),
	("model", KNeighborsRegressor())
])

pipe.fit(X, y)
pred = pipe.predict(X)
plt.scatter(pred, y)
```
![[ScaledNearestNeighborPipelineScatter.png]]