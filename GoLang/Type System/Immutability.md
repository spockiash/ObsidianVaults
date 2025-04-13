## Const
Go provides a way to declare immutable variable with `const` keyword instead of `var`:
```go
const x int64 = 10
```
Consts can be declared on package-level or in function. Just as with `var` you should declare const in a group of related constants within a set of parentheses. Unlike other languages constants in Go are limited in that they can be used only with built-in types. Expressions that consist of operators and the preceding values can also be used in constant assignment.

Go does not have a way to specify that a value calculated at runtime is immutable. There are also no immutable arrays, maps or structs. 
## Typed and Untyped consts
Untyped constant works just like a literal, it does have a default type when no other type can be inferred.
Typed constant can be directly assigned only to a variable of that type.

Untyped constants have more flexibility, for example numerical constants should be untyped for this reason.

Untyped constant declaration:
```go
const x = 10
//legal assignemnts
var y int = x
var z float64 = x
var d byte = x
```
Typed constants:
```go
const typedX int = 10
```
This constant can be assigned only directly to `int` type.
