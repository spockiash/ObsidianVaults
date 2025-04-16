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
The fields can be accessed via dot syntax:
```go
bob.name = "Bob"
```
The struct literal syntax cannot be mixed and matched, either all fields are specified or none of them are.
## Anonymous structs
Struct can be initialized to a variable without giving it a name, this is called anonymous struct:
```go
pet := struct {
	name string
	kind string
}{
	name: "Fido",
	kind: "Dog"
}
```
## Comparing and Converting structs
Structs are comparable only if all the fields are of comparable types. Go does not have extensibility to override this comparability. This could be done only via custom function.

Go allows for conversion between structs if the field type and order is the same. When dealing with anonymous functions it is possible to compare them to named structs:
```go
type firstPerson struct {
	name string
	age int
}
f := firstPerson{
	name: "Bob",
	age: 50,
}
var g struct {
	name string
	age int
}
// compiles -- can use = and == between identical named and anonymous structs
g = f
fmt.Println(f == g)
```