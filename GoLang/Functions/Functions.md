[[First class functions]]
[[Anonymous functions]]
[[Closures]]
[[Releasing resources with `defer`]]
# Declaring functions
Functions are declared with the `func` keyword, followed by the name of the function, then by parameters in parentheses and then by return type of the function:
```go
func div(num int, denom int) int {
	if denom == 0 {
		return 0
	}
	return num / denom
}
```
Just like other languages Go has `return` keyword that returns a value. Void functions do not need return statement.

Function that has no parameters has empty parentheses and empty return type.
## Named and optional parameters
Go does not have named and optional parameters. To simulate this feature we must use structs:
```go
type MyFuncOpts struct {
	FirstName string
	LastName string
	Age       int
}
func MyFunc(opts MyFuncOpts) error {
	// access fields here
}
```
## Variadic Input Parameters and Slices
Go has support for any number of parameters of a single type as variadic parameters. It must be of the same type and the variadic parameters must be last in the parameters declared or it must be the only parameter. It is signified with `...` before the type:
```go
func addTo(base int, vals ...int) []int {
	out := make([]int, 0, len(vals))
		for _, v := range vals {
			out = append(out, base+v)
	}
	return out
}
```
Under the hood this translates into slice and it can be called like this:
```go
fmt.Println(addTo(3))
fmt.Println(addTo(3, 2))
fmt.Println(addTo(3, 2, 4, 6, 8))
fmt.Println(addTo(3, []int{1, 2, 3, 4, 5}...))
```
Since it translates into slice, slice literal can be supplied as well but three dots must be put after the variable or literal of slice.
## Multiple return values
Go allows for multiple return values, they are defined in the return type declaration in function statement but they are supplied in parentheses divided by comma:
```go
func divAndRemainder(num, denom int) (int, int, error) {
	if denom == 0 {
		return 0, 0, errors.New("cannot divide by zero")
	}
	return num / denom, num % denom, nil
}
```
When returning from a function with multiple return values it is returned without the parentheses. All of them must be returned in correct order, separated by commas. The error in the example above is by convention always returned last.

Such function can be then assigned to values when calling by using the `:=`:
```go
result, remainder, err = divAndRemainder(5,2)
```
The returned values are discrete, it does not behave like Python with tuples as a result. The returned values can be ignored by using `_`:
```go
result, _, err = divAndRemainder(5, 2)
```
### Named return values
In contrast to other languages that support named input parameters, Go supports only named return values. When doing named return values they must be inside parentheses even if only one return value is used:
```go
func divAndRemainder(num, denom int) (result int, remainder int, err error) {
	if denom == 0 {
		err = errors.New("cannot divide by zero")
		return result, remainder, err
	}
	result, remainder = num/denom, num%denom
	return result, remainder, err
}
```
This basically predeclares the variables that will be used in the function as return values. The named values initialize to their zero value. This means they can be returned without assigning them values inside the function. 
### Blank returns
When we have function with multiple named return values we can do `return` without any parameter. This is called `blank` or `naked` return. What this does is returns the last values assigned to the return values. This can be used when handling errors so we can return the values in their zero value state. Blank returns are considered bad practice, because they make code harder to read.