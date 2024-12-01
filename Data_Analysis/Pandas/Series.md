In pandas Series is 1-D object for sequence of values of the same type and associated array or data labels called its index. The Series can be taught of as fix length ordered dictionary. The simplest Series is an array of data:
```python
obj = pd.Series([4, 7, -5, 3])
# 0    4
# 1    7
# 2   -5
# 3    3
# dtype: int64
```
Since we did not provide an index specification, the default is index 0 - n-1.  Information about the series can be obtained using `array` and `index` attributes:
```python
In [16]: obj.array
Out[16]:
<PandasArray>
[4, 7, -5, 3]
Length: 4, dtype: int64
In [17]: obj.index
Out[17]: RangeIndex(start=0, stop=4, step=1)
```
The `array` attributes result if `PandasArray` which usually wraps `NumPy` array.

# Creating series
## From Dictionary
If we have Python dictionary, we can create series from it:
```python
key_val_dict = { Ohio": 35000, "Texas": 71000, "Oregon": 16000, "Utah": 500 }
In [31]: obj3 = pd.Series(sdata)
In [32]: obj3
Out[32]:
Ohio 35000
Texas 71000
Oregon 16000
Utah 5000
dtype: int64
```
The series can be converted back with `to_dict()` method. By default when creating the series from dictionary, it respects the key as index. However custom labels can be provided:
```python
In [34]: states = ["California", "Ohio", "Oregon", "Texas"]
In [35]: obj4 = pd.Series(sdata, index=states)
In [36]: obj4
Out[36]:
California NaN
Ohio 35000.0
Oregon 16000.0
Texas 71000.0
dtype: float64
```
The California was missing in the original dictionary, so it filled it with value `NaN`, `missing` or `null` interchangeably. Since Utah in the original dictionary was missing in the label selection, it was excluded.

To figure out if there are missing values in Series  there are functions `pd.isna(data), pd.notna(data) and data.isna()`. Useful series feature is that it automatically aligns by index during arithmetic operations.
# Indexing
To create custom index we can create labels like with index parameter that accepts list:
```python
In [18]: obj2 = pd.Series([4, 7, -5, 3], index=["d", "b", "a", "c"])
In [19]: obj2
Out[19]:
d 4
b 7
a -5
c 3
dtype: int64
In [20]: obj2.index
Out[20]: Index(['d', 'b', 'a', 'c'], dtype='object')
```
Labeled series can be accessed with the label instead of indexes. For example:
```python
obj["a"]
-5
obj2[["c", "a", "d"]]
Out[23]:
c 3
a -5
d 6
dtype: int64
# 
```
The provided list is interpreted as list of indices.
Doing operations on arrays like filtering with Boolean array or applying other NumPy like features as math functions, will preserve the index-value link.

The series index can be altered by assigning new index list with same length.
## Series as dictionary
We can use series for example to find element with label:
```python
In [28]: "b" in obj2
Out[28]: True
In [29]: "e" in obj2
Out[29]: False
```
## Name attributes
Both Series object itself and its index have name attribute:
```python
In [43]: obj4.name = "population"
In [44]: obj4.index.name = "state"
In [45]: obj4
Out[45]:
state
California NaN
Ohio 35000.0
Oregon 16000.0
Texas 71000.0
Name: population, dtype: float64
```