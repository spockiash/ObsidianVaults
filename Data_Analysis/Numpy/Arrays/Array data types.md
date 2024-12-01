Data type of an [[Numpy ndarray]] is inferred from the data, or it can be specified when creating the array:
```python
arr1 = np.array([1,2,3], dtype=np.float64)
arr2 = np.array([1, 2, 3], dtype=np.int32)
```
Numpy in most cases provide mapping directly to the data structures in memory or disk. This enables numpy to connect directly to libraries written in other programming languages like C. The datatypes are named the standard way and their size is done by number suffix:
`float64 = double`
# Casting
To explicitly cast array to data type we can use `astype` method:
```python
arr = np.array([1,2,3,4,5])
float_arr = arr.astype(np.float64) # cast explicitly to float
```
Calling `astype` will always create new array even if the data is the same.

If we have strings in our data and want them to convert to numeric form we can do that as well:
```python
numeric_strings = np.array(y(["1.25", "-9.6", "42"], dtype=np.string_)
numbers = numeric_strings.astype(float) # float is alias for float64 in np
```

> [!warning] Numpy string truncates
> Numpy strings in array have fixed size and will truncate the data without warning. For better string support use Pandas.

When casting arrays we can use another arrays `dtype` as argument to `astype`:
```python
int_array = np.arange(10)
calibers = np.array([.22, .270, .357, .380, .44, .50], dtype=np.float64)
int_array.astype(calibers.dtype)
```
## Casting errors
If casting fails for some reason, like string cannot be converted to number, a `ValueError` will be raised. 
