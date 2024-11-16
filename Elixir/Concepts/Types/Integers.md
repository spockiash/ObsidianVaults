# Rounding and Truncate:
To round floating point value to get integer we can invoke the round function to get the closest integer. We can use the `trunc` function to get the integer part of float:
```elixir
round(3.58) #return 4
trunc(3.58) #return 3
```
# Checking for integer
Elixir provides ways for checking for type of a value. For example the predicate function `is_integer` can be used to check if value is an integer or not:
```sh
iex(11)> is_integer 4.5  
false  
iex(12)> is_integer 5  
true
```