# Basic setup
Pipelines can chain together operations to create single model. They can be invoked via:
```python
from sklearn.pipeline import Pipeline
#the pipeline accept list of tuples
pipe = Pipeline([
	("scale", StandardScaler()),
	("model", KNeighborsRegressor())
])
```