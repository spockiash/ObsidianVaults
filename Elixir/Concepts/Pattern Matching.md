Most basic form of pattern matching can be observed on the following example:
```elixir
[a, a] = [1, 1]
```
In this example we have two groups of two lists. The value of each element on both sides becomes bound to each other, so the first `a` will be bound to first number `1` in the list on right hand side.

Now lets consider assigning values `1` and `2` on the right hand side:
```sh
iex(3)> [a, a] = [1, 2]  
** (MatchError) no match of right hand side value: [1, 2]  
   (stdlib 6.1.2) erl_eval.erl:652: :erl_eval.expr/6  
   iex:3: (file)
```
The interactive shell told us that the right hand side does not match the left hand side. This is because the value of `a` is bound with value of 1. We must introduce new variable:
```sh
iex(3)> [a, b] = [1, 2]  
[1, 2]
```