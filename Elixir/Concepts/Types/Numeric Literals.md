# Special literals
Elixir supports shortcut notations for binary, octal and hexadecimal numbers:
```sh
iex(8)> 0b1010  
10  
iex(9)> 0o777  
511
iex(10)> 0x1F  
31
```
# Float literals
Float numbers require a dot followed by at lest one digit and also support `e` for scientific notation:
```sh
1.0
1.0e-10
```
Floats in Elixir are 64-bit in precision. Floats can be converted to integers with [[Integers#Rounding and Truncate|round and trunc]].
