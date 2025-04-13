Arrays are rarely used directly in Go. They are mainly used as backing data structure for other types like slices.
The most basic syntax for declaring an array is with `var` keyword and the type that is specified with size of the array in square brackets:
```go
var x [3]int
```
This creates array of three integers with all being zero value. To initialize values we use curly brackets after the type:
```go
var x = [3]int{10,20,30}
```
When we have sparse array (array where most values are 0) we can use indices to specify value at a position:
```go
var x = [12]{1, 5: 4,6, 10: 100, 5}
//[1, 0, 0, 0, 0, 4, 6, 0, 0, 0,
// 100, 15]
```
When initializing array from literals we can skip the size specifications and use `...` instead:
```go
var x = [...]{1,2,3}
```
## Multidimensional arrays
Go does not have true multidimensional array. We can simulate it with `[n][m]` syntax:
```go
var x [2][3]int
```
This declares an array of length 2 whose type is array of length 3. Go does not have true matrix support.
## Reading array
Like most languages Go uses bracket syntax to read array at position:
```go
x[0] = 10
```
Go does not support out of bounds index or negative index. It will cause compile time error or runtime panic.
## Limitations
Go arrays are rarely used explicitly because Go considers size of the array to be part of the type. This means array of different sizes are considered their own types. This also means we cannot use variables to specify array size, because it needs to be resolved at compile time.