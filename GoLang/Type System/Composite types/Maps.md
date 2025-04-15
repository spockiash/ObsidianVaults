Maps in Go are basically dictionaries. To create `nil` map we can use syntax:
```go
var nilMap map[string]int
```
This creates map with string keys and integer values. The zero value for map is `nil` with 0 length, attempting to read such map would result in 0 value for the type used. Writing to a `nil` map causes panic.

To create empty map that we can read and write to we have to use map literal:
```go
totalWins := map[string]int{}
```
This is an empty map literal. It has length of 0, but read and write operation is possible. Non empty map literal can look like this:
```go
teams := map[strings][]string {
	"Orcas": []string{"Fred", "Ralph", "Bijou"},
	"Lions": []string{"Sarah", "Peter", "Billie"},
	"Kittens": []string{"Waldo", "Raul", "Ze"},
}
```
In the map literal body we specify the key, follow it by `:` and then by the value literal. 

Maps are not comparable between each other. The key must be any comparable type, therefore slice cannot be used for this.
## `make`
Using `make()` function we can create empty map that has its size already defined:
```go
ages := make(map[int][]string, 10)
```
Such maps will have length of 0 at start and can grow past this size.

## The comma ok Idiom
To find out if key is in the map Go provides this idiom to find difference between a key that has 0 value and key that is not present in the map:
```go
m := map[string]int{
"hello": 5,
"world": 0,
}
v, ok = m["hello"]
v, ok = m["sun"]
```
The ok is boolean and will be `true` when the key is present and `false` when the key is not.
## Deleting map elements
Map element can be deleted with `delete(mapRef, key)` function:
```go
m := map[string]int{
"hello": 5,
"world": 0,
}
delete(m, "hello")
```
The delete function does not return value.
## Clearing maps
To remove all elements from map we use `clear(mapRef)` function:
```go
m := map[string]int{
"hello": 5,
"world": 0,
}
clear(m)
```
Unlike slices cleared maps have length of 0.
## Go maps as sets
Set is unordered list of unique elements. They are not present in go but can be simulated with maps:
```go
intSet := map[int]bool{}
vals := []int{5, 10, 2, 5, 8, 7, 3, 9, 1, 2, 10}
for _, v := range vals {
intSet[v] = true
}
fmt.Println(len(vals), len(intSet))
fmt.Println(intSet[5])
fmt.Println(intSet[500])
if intSet[100] {
fmt.Println("100 is in the set")
}
```
