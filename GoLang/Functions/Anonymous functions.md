Anonymous functions are nameless functions that are declared and defined inside another function. They cannot be declared at the package block outside functions or method. Instead of supplying the name, you can just do `funct(params) returnType {}`:
```go
func main() {
	f := func(j int) {
		fmt.Println("printing", j, "from inside of an anonymous function")
	}
	for i := 0; i < 5; i++ {
		f(i)
	}
}
```
It is illegal to provide name to anonymous functions. This means functions defined inside functions must be always anonymous. Named function can be declared only at package level or in structs as methods.

Anonymous functions can be called inline with declaration to avoid assigning them to variables.

Anonymous functions can be declared at the package level and assigned to variables:
```go
var (
	add = func(i, j int) int { return i + j }
	sub = func(i, j int) int { return i - j }
	mul = func(i, j int) int { return i * j }
	div = func(i, j int) int { return i / j }
)
```
Unlike normal functions, you can assign them a new value to a package-level. However package level function states should be immutable to make data flow easier to understand. 