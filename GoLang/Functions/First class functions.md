In go functions are a first class citizens.
# Functions as values
Functions are in fact values in Go, this means they can be assigned to variables and passed to other functions as parameters. Functions in Go are typed and the type is defined by their signature - parameters and return values. This means we can create a function variable like this:
```go
var myFuncVariable func(string) int
```
This variable can be assigned any function that matches the type:
```go
func f1(a string) int {
	return len(a)
}
func f2(a string) int {
	total := 0
	for _, v := range a {
		total += int(v)
	}
	return total
}

func main() {
	var myFuncVariable func(string) int
	myFuncVariable = f1
	result := myFuncVariable("Hello")
		fmt.Println(result)
	}
	myFuncVariable = f2
	result = myFuncVariable("Hello")
	fmt.Println(result)
}
```
The default zero value for a function variable is `nil`. Attempting to run `nil` function causes panic.
## Function type declaration
Instead of assigning to variables, functions can be declared as type in similar way to [[Structs]]:
```go
type opFuncType func(int, int) int
```
In this way the function type can be used in maps, slices and stuff like that. This way you can have multiple types