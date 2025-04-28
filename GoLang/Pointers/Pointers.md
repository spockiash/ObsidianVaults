[[Pointer performance]]
[[Pointers and mutability]]
[[Difference between maps and slices]]
[[Slices as buffers]]
# Primer
Pointer is a variable that holds location in memory where an item is stored. Every variable occupies contiguous memory location. Integers  that are 323 bits for example occupy 4 bytes in memory and booleans require single byte.

A pointer is a variable that contains the address where another variable is stored:
```go
var x int32 = 10
var y bool = true
pointerX := &x
pointerY := &y
var pointerZ *string
```
![[Pasted image 20250426133533.png]]
In Go pointers are usually 4 bytes in size, or on most modern hardware even 8 bytes. Pointer that points to nothing contains zero address. In Go the zero value for a pointer is `nil`.

The `nil` value is relevant for slices, maps and functions as a zero value, that is because they are implemented using pointers. In Go the `nil` is an untyped identifier that represents lack of a value for certain types. Unlike NULL in C, nil does not represent number 0.

The syntax is inspired by C/C++ pointers but without the memory management pain. Unlike C/C++ pointer arithmetic is not allowed in Go.
## The address operator
The `&` is the address operator, it returns the address where the value is stored:
```go
x := "hello"
pointer := &x // this creates pointer
```
It is used to create pointer from an variable.
## The indirection operator
The `*` is the indirection operator, it returns the value of where the pointer points to (the memory address):
```go
x := 10
pointer := &x // create pointer with address operator
valueAtAddress := *pointer // assigns the value stored at address of the pointer
```
This operation is also called dereferencing. Before dereferencing a pointer we must check if the pointer is non-nil. Otherwise panic occurs:
```go
var x *int
fmt.Println(x == nil) // true
fmt.Println(*x) // panic
```
## The pointer type
Pointers are typed, to create variable of a pointer type simply write the type with `*` before the type name:
```go
var str_ptr *string
```
There is a built in function `new` creates a pointer variable:
```go
var x = new(int) 
fmt.Println(x == nil) // prints false
fmt.Println(*x) // prints 0
```
It creates a pointer to a zero value instance of the provided type. However this function is rarely used in Go. When dealing with struct literals we can create a pointer from them using the `&` operator. With primitive types like numbers, booleans and strings this is not possible, so we need to declare normal variable first:
```go
x := &Foo{}
var y string
z := &y
```
## Handling constants
In Go not being able to take the address of a constant can be issue. If you have a struct with a field that is of pointer to a primitive type, we cannot assign it with literal value directly:
```go
type person struct {
	FirstName string
	MiddleName *string
	LastName string
}

p := person {
	FirstName: "Jordan"
	MiddleName: "B" // this wont compile
	LastName: "Neterson"
}
// cannot use "Perry" (type string) as type *string in field value
```
There are two ways around this, create a variable first that we pass to the struct or create a helper function that can create pointer from literal value:
```go
func makePointer[T any](t T) *T{
	return &t
}
p := person{
	FirstName: "Pat",
	MiddleName: makePointer("B"), // This works
	LastName: "Peterson",
}
```
This works because parameters to functions are variables and those have addresses.
## Pass by value
In languages like Java and JavaScript there is a difference in behavior between primitive types and classes. Python for example does not have primitive values, instead it uses immutability of instances to simulate them.

When the primitive value is assigned to another variable or passed to some functions as parameter any changes in those copies will not have effect on the original:
```java
int x = 10;
int y = x;
y = 20;
System.out.println(x); // prints 10
```

When we look at what happens to classes in for example Python we can see the difference:
```python
class Foo:
	def __init__(self, x):
		self.x = x

def outer():
	f = Foo(10)
	inner1(f)
	print(f.x)
	inner2(f)
	print(f.x)
	g = None
	inner2(g)
	print(g is None)

def inner1(f):
	f.x = 20
	
def inner2(f):
	f = Foo(30)

outer()
```
Running this will get output of :
```sh
20
20
True
```
That is because the following is the case in languages like Python, Java or Ruby:
* If you pass an instance of a class to a function and you change the value of a field, the change is reflected in the variable that was passed in
* If you reassign the parameter, the change will not be reflected in the variable that was passed in
* If you pass `nil`/`null`/`None` for a parameter value, setting the parameter itself to a new value does not modify the variable in the calling function

Some people explain this that the languages use pass by reference for classes instances. If this would be the case the examples above would change the variable in the calling function. These languages always pass by value like Go. This explanation is not lie, it just leaves out the technical under the hood detail about how the pass by value works. 

What is seen is that every instance of a class in these languages is implemented as a pointer. When class instance is passed to a function or method, the value being copied is the pointer to the instance. Since `outer` and `inner1` are referring to the same memory, changes made to fields of the class instance are reflected in the outer variable. When the value is reassigned to a new instance, this creates a separate instance that does not affect the outer variable.

In Go this is exactly the same, only Go give you a choice whether to pass pointers or values.

## Pointers indicate zero value
Go pointers are often used to indicate the difference between variable of field that has been assigned with the zero value and those where it was not assigned a value at all. For this purpose the `nil` pointer should be used to represent unassigned variable or struct field.

When doing this pattern it is better to use the [[Maps#The comma ok Idiom|comma ok idiom]] that can be seen in maps. Instead of returning the `nil` pointer from a function return the value and the boolean. The `nil` pointer cannot be passed into a function as parameter as the value cannot be changed.
