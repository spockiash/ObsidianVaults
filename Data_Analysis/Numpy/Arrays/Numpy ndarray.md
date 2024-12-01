Numpy N-dimensional array is fast and flexible container for large datasets. They provide ways of doing operations, [[Numpy array arithmetic|arithmetic]], [[Indexing and slicing]] on whole blocks using similar syntax as [[Scalar types|scalar]] objects.

Below is an example how an ndarray can be created and how batch computation works:
```python
data = np.array([[1.5,-0.1, 3], [0, -3, 6.5]])
data
# array([[ 1.5, -0.1,  3. ],
#      [ 0. , -3. ,  6.5]])
data * 10
# array([[ 15.,  -1.,  30.],
#      [  0., -30.,  65.]])
```

Numpy ndarray is **homogeneous**, meaning all data must be of same type. Every array has a shape attribute: tuple indicating size:
```python
data.shape
# (2, 3)
```
# Creating ndarrays
The easiest way of creating an array is using array function. It accepts any sequence like object and converts it to an ndarray, for example list:
```python
ls = [1, 2, 3, 4, 5, 6, 7, 8, 9]
data1 = np.array(ls)
data1 # array([1, 2, 3, 4, 5, 6, 7, 8, 9])
```
 nested sequences like list of equal-length lists will be converted into a multidimensional array:
 ```python
 data2 = [[1, 2, 3, 4], [5, 6, 7, 8]]
 arr2 = np.array(data2)
 # [[1, 2, 3, 4], [5, 6, 7, 8]]
```

## Other ways of creating ndarrays
There are other methods that can create arrays, for example `np.zeros` that will create all zero array based on provided shape or number of rows:
```python
arr3 = np.zeros(10) # create 1d array with 10 zeros
arr4 = np.zeros((2,6)) # create 2d array with 6 zeros on each dimension
```
There are other methods like empty that creates uninitialized array. Then there is `np.ones` and so on. For creating multidimensional array pass tuple with shape.

> [!tip] Empty does not create zeros
> Calling `np.empty` does not ensure zeros. It forms uninitialized array and there can be garbage data.
### Range
The `np.arange` is an array creation method that will create array with values 0-range. It is similar to python build-in range function.

### Important array creation functions
* `array` - convert input to an ndarray
* `asarray` - convert input to ndarray, but do not copy if the inputs are already ndarray
* `arange` - returns ndarray with values in range 0- range
* `ones` - create array of ones with specified size or shape
* `ones_like` - creates array from another array but with ones with the same shape
* `zeros` - create array of zeros with specified size or shape
* `zeros_like` - creates array from another array but with zeros with the same shape
* `empty` - create array of uninitialized values with specified size or shape
* `empty_like` - creates array from another array but with unin. values. with the same shape
* 
* `full` - create array of specified fill value with specified size or shape
* `full_like` - creates array from another array but with fill value
*  `eye, identity` - Creates N x N identity matrix (1 on diagonals, 0 elsewhere)
## Verifying size
To verify size we can use the shape attribute or ndim attribute:
```python
arr2.ndim # 2
arr2.shape # (2,3)
```
# Array data types
Unless specified the array will infer [[Array data types|data type]] from the passed data from which it creates the array. The data is stored in special `dtype` metadata object:
```python
data.dtype # dtype('float64')
arr2.dtype # dtype('int64')
```