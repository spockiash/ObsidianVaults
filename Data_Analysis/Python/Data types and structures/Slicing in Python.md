# Slice Operator
The slice operator is used to select slice from types like lists, tuples, strings and even [[Indexing and slicing|numpy]] types. The syntax is:
```python
arr[start:stop]
```
* The `start` is index where slicing starts (inclusive)
* The `stop` is index where slicing stops (inclusive)
If either of them is omitted the default behavior is:
* `start`: Defaults to 0
* `stop`: Defaults to the length of an array
Python arrays are indexed from zero.