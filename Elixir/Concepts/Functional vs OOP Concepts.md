In object oriented programming consider following statement:
```
	a = 1
```
In languages like C++ or C# this statement means variable `a` is assigned with value 1. However in languages like Elixir this is not the case. In Elixir this notation is more inline with mathematics as `a` equals to 1. Meaning `=` is literally equality operator and using it means left hand side is equal to right hand side. This means the following statements are equivalent:
```elixir
	a = 1
	1 = a
```
Another important aspect of functional programming is [[Immutability|immutability]] of data. This goes hand in hand with stateless functions.

