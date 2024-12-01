# Check for missing values
Missing values can be checked with `isna(), isnull() and any()` functions:
```python
import pandas as pd
import numpy as np

# Example DataFrame
data = {
    "A": [1, 2, 3],
    "B": [4, np.nan, 6],
    "C": [7, 8, 9]
}
df = pd.DataFrame(data)

# Check if any NaNs exist in the DataFrame
contains_nan = df.isna().any().any()
print(contains_nan)  # Output: True
```
## Check for Missing Values by Column
If you want to see which specific columns contain `NaN`, you can call `.isna().any()` without the second `.any()`:
```python
# Check column-wise for NaN
print(df.isna().any())
```
## Check Total Missing Values
```python
# Count total NaN values
total_nan = df.isna().sum().sum()
print(total_nan)  # Output: 1
```
## Ensure there are no NaN values
If you want to confirm there are absolutely no `NaN` values in the DataFrame, use `.notna().all()`:
```python
# Check if the entire DataFrame has no NaN values
no_nan = df.notna().all().all()
print(no_nan)  # Output: False
```
