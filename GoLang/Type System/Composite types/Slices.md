Unlike arrays, Go slices can grow in size as needed. Size of the slice is not part of its type. The syntax is almost the same as arrays but we do not specify its size:
```go
var x = []int{10, 20, 30}
```
This creates a slice of size 3 with slice literals. As in arrays we can also use indexing to create sparsely initialized slice:
```go
var x = []{1, 5: 4,6, 10: 100, 5}
//[1, 0, 0, 0, 0, 4, 6, 0, 0, 0,
// 100, 15]
```
Multidimensional can be simulated with `[][]`:
```go
var x [][]int
```
## The `nil` value
When we create slice without using literal we get slice of value `nil`:
```go
var x []int
```
The `nil` is used with some types to represent no value. It is untyped, so it can be used to compare with other types
## Comparing slices
Slice is not comparable type with operator `==`, the only thing that can be compared to is `nil`. To compare slices the Go slices package contains functions for that fore example `slices.Equal(x, y)`. It requires the elements of the slices to be comparable.

Go also offers package reflect that has `DeepEqual` function. This is legacy function and is intended for the use in tests.
## Function `len`
This function returns the size of a slice:
```go
var slice = []int{}
len(slice)
```
## Append slices
Appends is used to grow slices. The `append` function takes at least 2 parameters and returns slice of the same type. As first argument it takes the slice to be appended and as second value it takes the value of the slice type:
```go
var slice = []int
slice = append(slice, 10)
```
It is possible to append multiple values at one:
```go
var x = []int{1,2,3}
x = append(x, 5,6,7)
```
One slice can be appended to another using the `...` operator to expand the source slice:
```go
var x = []int{1,2,3}
var y = []int{10,20,30}
x = append(x, y...)
```
It is a compile-time error when append is not assigned to variable. This is because Go is call-by-value language. Every time we pass a parameter to a function, Go makes a copy of the value that is passed in. Passing a slice to the append makes a copy of the slice for the function. It then modifies the copy of the slice and returns it. Then we have to assign it.
## Capacity
Capacity is a value that represents number of locations in memory where elements of the slices are reserved. The capacity can be greater then lengths, which is the number of slice elements. When the length reaches capacity, there is no more room to put values.

When additional values are added to slice at full capacity, Go runtime allocates new backing array for the slice with a larger capacity. The values of the original backing array are copied to this new one and the slice is updated to refer to the new backing array.

This creates some overhead, therefore Go usually creates reserve space for the backing array size. The rule as of Go 1.18 is to double the capacity of a slice when the current capacity is less than 256.

The built-in `cap` function returns the capacity of an slice. This function is useful when manually managing slices and to decide if slice is large enough or if to call make function.
```go
var x []int
cap(x)
```
This function works with arrays as well but it will produce the same result as `len`.
It is more efficient to size the slices once with `make` function.
## Function `make`
Function `make` is useful for creating sized slices. It takes as arguments the type, size and optionally capacity:
```go
x := make([]int, 5)
```
This creates slice of length 5 of type int.
Appending values to such slice will assign the value after the first 5 elements:
```go
x = append(x, 10)
```
This would produce slice with content: `[0,0,0,0,0,10]` with size 6 and capacity 10. The capacity was doubled as soon as the sixth element was added.
### Append to empty slice
If we create slice with non-zero capacity and length of 0, it cannot be indexed into but append will insert values to the slice starting at index 0.
```go
x := make([]int, 0, 10)
x = append(x, 5,6,7,8) // [5,6,7,8]
```
## Clearing slices
To empty an slice we can call `clear(s)` function. It takes reference to a slice and resets its elements to zero:
```go
var x = []string{"first", "second", "third"}
clear(x) //returns slice with 3 empty strings, len = 3
```
## Slicing
If we want to slice a slice we can use the square brackets syntax and instead of index we can put there starting and ending offset separated by `:`, the boundaries can be omitted and this way we select whole slice to the left or right:
```go
x := []string{"a", "b", "c", "d"}
y :=[:2] // a, b
z :=[1:] // b, c, d
d :=[1:3] // b, c
e :=[:] // a, b, c, d
```
When taking slice from the slice, the result is a reference to the sub slice in the slice as a whole. This means multiple variables then point to the slice. Modifying sub slices will modify the original slice as well.

We cannot use append on sub slices as it will cause unintended consequences. It might overwrite the part of the whole slice when we append to sub slice. The solution to this is to either never use append on sub slices or to use full slice expression. This is number after the slice separator:
```go
x := make([]string, 0, 5)
x = append(x, "a", "b", "c", "d")
y := x[:2:2]
z := x[2:4:4]
```
It acts as a guard against overriding the entire slice.
## Copy
This function takes two parameters, the first is destination slice and second i source slice. The size of the resulting slice is limited by the smallest slice passed onto the function. It returns length of the slice:
```go
x := []int{1, 2, 3, 4}
y := make([]int, 4)
num := copy(y, x)
fmt.Println(y, num)
```
We can use this property to copy sub slice, if the destination slice is of capacity 2 and source is larger it will take only first 2 items from the slice:
```go
x := []int{1, 2, 3, 4}
y := make([]int, 2)
num := copy(y, x)
```
We can also copy from the middle of the source slice:
```go
x := []int{1, 2, 3, 4}
y := make([]int, 2)
copy(y, x[2:])
```
## Converting arrays to slices
To convert entire array to slice use the syntax `[:]`:
```go
x := [4]int{5,6,7,8}
y := x[:] //converts array to slice
```
## Converting slices to arrays
We can use type conversion to do this:
```go
xSlice := []int{1, 2, 3, 4}
xArray := [4]int(xSlice)
```
