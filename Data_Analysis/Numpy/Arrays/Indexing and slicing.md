In numpy one dimensional arrays act as lists in python:
```python
arr = np.arange(10)
arr[3:5]
# array([3, 4])
```
This slicing is using [[Slicing in Python#Slice Operator|slice operator]] to retrieve selection from the data by start and stop indexes. The start is inclusive and stop is exclusive.
```python
arr = np.arange(10)
# array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
arr[3:5]
# array([3, 4])
arr[:5] # returns array 0-4
arr[5:] # returns array 5-9
```

# Simple broadcasting
When we use the slice operator to assign scalar value. This will broadcast or propagate the value to the entire selection:
```python
arr[5:8] = 12 # array([ 0,  1,  2,  3,  4, 12, 12, 12,  8,  9])
```

> [!warning] Important distinction
> Important distinction between built-in  Python lists. Numpy slice operation does not create **new** array. Instead it acts on **view** of the original array. Meaning the original array is affected as opposed to built-in types that create new.

This can be demonstrated here:
```python
arr = np.arange(10)
arr[5:8] = 12
arr_slice = arr[5:8]
arr_slice
# array([12, 12, 12]) - this is not new array, it is the view of the original
arr
# array([ 0,  1,  2,  3,  4, 12, 12, 12,  8,  9])
# as you can see, the original array is changed when we manipulated view of     # arr_slice
rr_slice[:] = 64 # array([ 0, 1, 2, 3, 4, 64, 64, 64, 8, 9])
```
Numpy does this because it is designed for large datasets and copying is memory expensive.
## Explicit copy
If we want to actually copy the data, we can explicitly call `copy` method after the slice operator:
```python
arr[5:8].copy()
```
# Higher dimensional arrays
In n-D arrays the elements at each index is not scalar but rather 1-D array representing column of the n-D array. They can be indexed in comma separated list of indices to select individual elements:
```python
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
arr2d[2] # array([7, 8, 9])
```

To select individual element:
```python
arr2d[0][2] # 3
arr2d[0,2] # 3
```
Both statements are equivalent. The axis are indexed from 0 to n. So Axis 0 is like row, Axis 1 is like column in 2-D array. In higher dimensional arrays if we omit latter selections we will get lower n-D array of the data along the higher dimensions:
```python
arr3d = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
arr3d
# array([[[ 1, 2, 3],
# [ 4, 5, 6]],
# [[ 7, 8, 9],
# [10, 11, 12]]])
arr3d[0]
# array([[1, 2, 3],
# [4, 5, 6]])
```

> [!warning] Numpy is different
> This way of dealing with n-D arrays in numpy will not work on Python built-in objects.

## Assigning
Both scalar values and arrays can be assigned to `arr3d`:
```python
ld_values = arr3d[0].copy()
arr3d[0] = 42
# array([[[42, 42, 42],
# [42, 42, 42]],
# [[ 7, 8, 9],
# [10, 11, 12]]])
```
When we provide more indices, we can get 1-D array from 3-D array:
```python
arr3d[1, 0] # array([7, 8, 9])
```
## Indexing with slices
Consider the following array:
```python
arr2d
# array([[1, 2, 3],
#       [4, 5, 6],
#       [7, 8, 9]])
arr2d[:2]
# array([[1, 2, 3],
#       [4, 5, 6]])
```
When selecting with slice operator 2-D array with `[:2]` it sliced along axis 0. Slice therefore selects range of elements along an axis. The `[:2]` can be read as select the first two rows of `arr2d`. But multiple slices can be passed:
```python
arr2d[:2, 1:]
# array([[2, 3],
# [5, 6]])
```
The first term is the same as above, it selects first two rows. The second therm is selection for axis 1. Therefore it selects `2x2` right upper corner of the 2-D array. It can be read as select from rows and select from columns.

When slicing like this we always get the **view** that matches the dimensions. By mixing indexes and slices we can get lower dimensional slices. For example we can select second row but only the first two columns:
```python
ower_dim_slice = arr2d[1, :2]
```
We can select all by doing `[:]`, based on if we want to select rows or columns here is guide from Python for Data Analysis book:
![[Python for Data Analysis_Indexing_NDARR.png]]
