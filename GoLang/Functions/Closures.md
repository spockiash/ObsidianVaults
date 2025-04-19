Closures are functions declared inside functions that are able to access outside scope variables of the outer function.
# Passing Functions as Parameters
Functions can be passed as parameters to other functions. For example the standard library has a function called `sort.Slice` that takes any slice and a function that is used to sort the slice that is passed:
```go
// sort by last name
sort.Slice(people, func(i, j int) bool {
	return people[i].LastName < people[j].LastName
})
```
The closure passed as a parameter has two parameters `i` and `j`, but within the closure we use the parameter value from `people`. This is called capturing a variable by the closure.
# Returning a function
Go allows for returning a function from a function:
```go
func makeMult(base int) func(int) int {
	return func(factor int) int {
		return base * factor
	}
}
```
Closures over all are very useful in go.