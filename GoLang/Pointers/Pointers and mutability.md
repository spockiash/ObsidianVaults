# Pointer indicate mutability
Mutability is tied with pointers in Go. They can be used to mark mutable parameters to a function. In Go when we pass pointer to a function as parameter, the function gets a copy of the pointer. The pointer still points to the same location, but we have new pointer inside the function.
## Passing `nil` pointer to a function
When we pass `nil` pointer to a function, the value cannot be made non-`nil`. The value can be reassigned only if there was a value already assigned to the pointer.
## Dereferencing in functions
When we have a copy of the pointer and want to change the value of the object where the pointer points, we have to dereference the value. Dereferencing modifies the value stored at the memory location that both the original and the copy of the pointer reference:
```go
func failedUpdate(px *int) {
	x2 := 20
	px = &x2
}
func update(px *int) {
	*px = 20
}
func main() {
	x := 10
	failedUpdate(&x)
	fmt.Println(x) // prints 10
	update(&x)
	fmt.Println(x) // prints 20
}
```
Here we start with value x of 10, the `failedUpdate` function takes pointer of the `x` value and makes copy, we then assign to the copy of the pointer  called `px` new value but this value ceases to exist when the scope of this function ends. Then we print the value after `failedUpdate` call and see the value of the variable `x` in the outer scope did not change.

After calling the `update` function and we dereference the pointer with `*` operator and assign it new value of 20. The dereferencing operation points us to the memory location of the outer variable `x` and can be used to assign value.