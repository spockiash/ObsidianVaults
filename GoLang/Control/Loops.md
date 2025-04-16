Go provides only `for` as a keyword for loops. Therefore it provides different styles of `for`.
# Complete statement
C like for loop, it uses `:=` for declaration as var is not legal in loop control variable declaration:
```go
for i := 0; i < 10; i++ {
	fmt.Println(i)
}
```
The comparison part needs to be an expression that evaluates to type bool, it is checked immediately before each iteration of the loop. If the expression evaluates to `true` the iteration will execute.

The last part is an assignment that occurs after the iteration, before condition evaluation. The initialization and the assignment can be skipped:
```go
i := 0
for ; i < 10; i++ { // skip init
	fmt.Println(i)
}

for i := 0; i < 10; { // skip assignment, custom compute inside loop
	fmt.Println(i)
	if i % 2 == 0 {
		i++
	} else {
		i+=2
	}
}
```
# Condition-Only `for` statement
This is basically a `while` from other languages, with just a condition it will iterate until the condition evaluates false:
```go
i := 1
for i < 100 {
	fmt.Println(i)
	i = i * 2
}
```
# The infinite `for` statement
This is just an infinite loop, it runs indefinetly:
```go
for {
	fmt.Println("Hello")
}
```
# The `break` and `continue`
The `break` will cause immediate exiting of the loop. Any loop can be broken out of. The `continue` will skip the current iteration and jumps to the next.
Using `break` and `continue` to control flow in loops is idiomatic in Go.
# The `for-range` statement
This structure resembles iterators from other languages. It takes two variables into the loop and some data structure for the range part:
```go
evenVals := []int{2, 4, 6, 8, 10, 12}
for i, v := range evenVals {
	fmt.Println(i, v)
}
```
The first variable `i` is the index position and the `v` is the value at the position. So for example `i=0 -> v=2` and so on. When looping over an array, slice, or string, an i for index
is commonly used. When iterating through a map, k (for key) is used instead.
When the variable is not needed for example the index we can use a `_` as a name for it. Go will ignore this value.