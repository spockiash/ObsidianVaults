Maps are implemented as pointers to a struct. Passing a map to a function means pointer is copied. Having maps for input type in a function parameter is bad idea in Go. The reason is they provide no information on the values held within them. Nothing explicitly defines the keys to a map, so using them makes the code harder to read. Structs should be used instead.

Passing slice to a function in Go is more complicated. Slices are implemented as a struct that has 3 fields:
* pointer to array
* length
* capacity
When we change passed slice in a function the change is reflected in the outer variable. But when we use append this is not the case. This is because changing the values in the slice changes the memory that the pointer points to.

When doing appends to a slice and there is enough capacity what happens is the original outer slice will still point to the location but since the changes to length was done to a copy of the slice struct, the original slice variable does not see the changes. This is because the length of the original slice is still the same.

When the append is done to a slice with less capacity, the capacity and length are changed on the copy also so the original value does see the changes. The copy now points to entirely different part of memory.

Therefore good practice is to assume functions cannot change slices unless it is specified in documentation as otherwise.

