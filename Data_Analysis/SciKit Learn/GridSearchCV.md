This object can be found in model_selection library:
```python
from sklearn.model_selection import GridSearchCV
```
When creating an GridSearchCV object we need to pass an estimator as parameter. Estimator is something that has fit and predict functions such as pipeline. Next argument is parameter grid. Parameter grid represents all the settings we want to go through in our pipeline.

# GridSearchCV estimator settings
To find the possible settings of our estimators we have function `.get_params()`. For example when we call this on pipe we can get the following result:
```python
pipe = Pipeline([
	("scale", StandardScaler()),
	("model", KNeighborsRegressor())
])

pipe.get_params()
#result
{'memory': None,
 'steps': [('scale', StandardScaler()), ('model', KNeighborsRegressor())],
 'verbose': False,
 'scale': StandardScaler(),
 'model': KNeighborsRegressor(),
 'scale__copy': True,
 'scale__with_mean': True,
 'scale__with_std': True,
 'model__algorithm': 'auto',
 'model__leaf_size': 30,
 'model__metric': 'minkowski',
 'model__metric_params': None,
 'model__n_jobs': None,
 'model__n_neighbors': 5,
 'model__p': 2,
 'model__weights': 'uniform'}
```
In our example case below we are interested in finding best setting for `model__n_neighbors` however we can test for more estimator settings as well.

## Cross-validation
Cross-validation will create n-folds of data. It will use 1/n splice for predicting and the rest for training. The higher the number, the more folds and potentially more robust model.
However one must ensure that the data in each splice is diverse and equally represented.
## Example
Considering California dataset from the introduction, we can use GridSearchCV to setup a model that will test and cross-validate our pipeline. And doing so create more robust model:
```python
import sklearn
import pandas as pd
from sklearn.datasets import fetch_california_housing
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsRegressor
from sklearn.model_selection import GridSearchCV
import matplotlib.pylab as plt

X, y = fetch_california_housing(return_X_y=True)

pipe = Pipeline([
	("scale", StandardScaler()),
	("model", KNeighborsRegressor())
])

#estimator is object that can fit and predict
#param_grid is what parameter we are finding the best setting for
#cv stands for cross-validation and it will crossvalidate the data
mod = GridSearchCV(estimator=pipe,
    param_grid={'model__n_neighbors':[1,2,3,4,5,6,7,8,9,10]},
    cv = 3)
mod.fit(X,y)
#creates pandas data frame
pd.DataFrame(mod.cv_results_)
```
In this example we can create fairly robust model from fairly little lines of code. Below is output of the pipeline using `cv_results_`:
![[GridSearchResultExample.png]]
![[GridSearchResultExample2.png]]
Here description of the data columns:
* `mean_fit_time` - The average time (sec.) taken to fit the pipeline across all cross-validation folds for this particular hyperparameter combination
* `std_fit_time` - standard deviation of the fit time. Low value indicates consistent training times across folds
* `mean_score_time` - The average time taken to evaluate the model on the test set for each fold
* `std_score_time` - Standard deviation of the scoring time across folds
* `param_model_n_neighbors` - The value of hyperparameter being tested. This shows which hyperparameter combination this row corresponds to.
* `params` - A dictionary showing the exact hyperparameter configuration for this row
* `split0_test_score, split1_test_score and split3_test_score` - The models performance score (R^2 by default for regressors) on the test set for each of the three cross-validation splits. Each split corresponds to training on two parts of the data and testing on the third. 
* `mean_test_score` - The average score across all cross-validation splits for this hyperparameter configuration. This is a key value used by GridSearchCV to determine the best hyperparameters.
* `std_test_score` - The standard deviation of the test scores across the splits. Showing how much the model's performance varied across folds. Lower values indicate consistent performance.
* `rank_test_score` - The rank of this hyperparameter combination based on the `mean_test_score`.