Structs is user defined type. It has syntax `type structName struct { members }`:
```go
type person struct {
	name string
	age int
	pet string
}
```
Structs can be defined inside or outside of a function. If defined inside it can be used only in that function.
Struct can be declared with `var`:
```go
var fred person
```
This struct is created with all fields set to its zero value. To create struct variable from literal we can do:
```go
bob := person{}.
julia := person{
	"Julia",
	40,
	"cat",
}
```
