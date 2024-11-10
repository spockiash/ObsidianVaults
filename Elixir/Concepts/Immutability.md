All data types in Elixir are immutable. If we consider statement `a = 1` what happens is that the match operator `=` bounds value 1 to `a`., but what happens here:
```sh
iex(5)> a = 1  
1  
iex(6)> a = 2  
2
```
Whenever we use the match operator, it takes the right hand side and bounds it to the left hand side. This behavior can be changed using the pin operator `^`:
```sh
iex(8)> ^a = 3  
** (MatchError) no match of right hand side value: 3  
   (stdlib 6.1.2) erl_eval.erl:652: :erl_eval.expr/6  
   iex:8: (file)
```
This ensures the value will match the original value. When we change the order and put on the left had side literal value and on right side `a` we get:
```sh
iex(8)> 3 = a  
** (MatchError) no match of right hand side value: 2  
   (stdlib 6.1.2) erl_eval.erl:652: :erl_eval.expr/6  
   iex:8: (file)  
iex(8)> 2 = a  
2
```
The `3 = a` fails with error, because a has value 2 bound to it and the match will result in error.
## Benefits of immutability
Immutable data means it can be easily shared between processes. This helps with scalability as the data never changed between operations.