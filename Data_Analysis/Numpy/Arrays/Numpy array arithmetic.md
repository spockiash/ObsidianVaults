Numpy uses **vectorization** instead of loops and provides way to express batch operations on data. Any arithmetic done on same size arrays will apply the operation element-wise:
```python
 arr = np.array([[1., 2., 3.], [4., 5., 6.]])
 arr * arr # mutliplies all the elements with each other
 arr - arr # subtract all elements, result will be 0s 
```

Operations with scalars will propagate the argument to each element in the array:
```python
data = np.array([[1.5,-0.1, 3], [4, -3, 6.5]])
1/data
# array([[  0.66666667, -10.        ,   0.33333333],
#      [  0.25      ,  -0.33333333,   0.15384615]])
```

Comparison between arrays of the same size will yield Boolean array result:
```python
data1 > data # results in array of boolean values based on the comp. res.
```
