# Everything is an object
Python uses object model. Every data type is considered by the interpreter its own object referred to as Python object. Each object has its own internal data and associated type.
# Dynamic references and strong types
Variables in python a do not have inherent type associated with them. This means we can assign to them any type we want. However python is strongly typed object.

This means once we have a variable with assigned object of some type, we cannot implicitly cast it to different type. We cannot pass number to function expecting string without explicit cast.

Implicit conversions can occur only when certain circumstances are permitted such as converting between integer and float:
```python
a = 4.5
b = 2
print(a/b) # prints 2.25 b is implicitly converted from integer to float
```

## Determining type of object
We can use `isinstance(val, type)` to determine if an object is of type:
```python
a = 5
isinstance(a, int) # returns True
```
We can pass tuple of types to check if the type is presented in the provided collection inside tuple:
```python
isinstance(a, (int, float)) # returns True
```
# Attributes and methods
Objects in Python have typically both attributes and methods. Attributes provide access to other objects inside an object and methods provide functions associated with the object and typically have access to inner elements of the object. The syntax is:
```python
obj.attribute_name
obj.method_name(..)
```
Attributes and methods can be accessed by name via the `getattr` function:
```python
getattr(a, "spit")
```
# Duck typing
Often you may not care about the type of an object, but rather only whether it was certain methods or behavior. This is called `duck typing` because of the saying “If
it walks like a duck and quacks like a duck, then it’s a duck...”. For example we can determine if object is iterable if it implements iterator protocol. For many object it means it has an `__iter__ ` method associated. Alternative way is to try using the protocol itself:
```python
def isiterable(obj)
	try:
		iter(obj)
		return True
	except TypeError:
		return False
```
# Modules
Python module is python file containing Python code. For example if we have `some_module.py` in the same directory, we can use import to get the exposed functionality:
```python
import some_module
some_module.do_stuff() #call the module
```
