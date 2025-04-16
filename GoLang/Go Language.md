Go is statically and strongly typed language. It is compiled and does have garbage collector.
# Types and declarations
## Type system
Go has [[Pre-declared (built-in) types|built-in]] types and [[Composite types|composite]] types.
## Declarations
Go has multiple ways of declaring variable. The most verbose way of declaring variable is with var keyword:
```go
var x int = 10
```
We van skip the type when using literals, because literal integer will default to being `int`:
```go
var x = 10
```
This also means we can use the default zero value with type:
```go
var x int
```
Multiple variables can be declared at the same time:
```go
var x, y int = 10, 20
```
Go allows for declaring multiple types at once:
```go
var x, y = 10, "hello"
```
Go also supports declaration lists:
```go
var (
x int
y = 20
z int = 30
d, e = 40, "hello"
f, g string
)
```
### Short declaration
Go also supports short declaration and assignment format. In function we can replace `var` with `:=` operator:
```go
var x = 10
x := 10
```
We can also do the multi variable declaration on the same line:
```go
var x, y = 10, "hello"
x, y := 30, "hello"
```
This short declaration operator can also assign new value to existing variables:
```go
x := 10
x, y := 30, "hello"
```
This operator has limitation, because it cannot be used outside of a function. Therefore it cannot be used in modules. Therefore the most common way in go is using := inside functions and `var` outside.
#### When to use var in function
There are situations where using `var` in function is better:
* When initializing variable with zero value
* When assigning an untyped constant or literal to a variable and the default type for the constant is different type from what we want
* When we want to avoid shadow variables
### Variables in module block
Variables outside of a function should be made [[Immutability|immutable]]. As changing package-level variable can create side effects.
## Unused variables
In go unused variables are considered compile-time error. Declared variable must be read at least once.
Unused constants are allowed as they are calculated during compile-time and cannot have any side effects.
# Control structures
[[Program structures]]