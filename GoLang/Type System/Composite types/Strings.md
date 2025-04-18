Strings are not arrays of runes in Go but raw sequences of bytes. Go strings do not have any encoding but many libraries assume UTF-8 encoding. They are also immutable.
## Extracting bytes
We can extract bytes using the square bracket syntax with index just like array or slice:
```go
var s string = "Hello world"
var b byte = s[6]
```
The result will be byte with value of 116 which is lowercase t in UTF-8 encoding. When the character encoded in the string is larger than 1 byte (special symbols, emojis) then we would get only 1 byte on that position with index. This would break the logic, so direct indexing with strings is not recommended.
## Converting string to runes
Single rune can be converted with `string()` function:
```go
var a rune = 'x' // can be rune or byte
var s string = string(a)
```
String can be converted to slice of bytes or runes:
```go
var s string = "Hello, world";
var bs []byte = []byte(s)
var rs []rune = []rune(s)
```
## Iterating over strings
To iterate over strings we use the [[Loops#The `for-range` statement|for-range]]:
```go
sampes := []string{"hello", "applne_π!"}
for _, sample := range samples {
	for i, r := range sample {
		fmt.Println(i, r, string(r))
	}
	fmt.Println()
}
```
The output when the code iterates over the word hello:
0 104 h
1 101 e
2 108 l
3 108 l
4 111 o
For the second word we get the expected result except when we come to the value of π:
...
5 90 _
6 940 π
8 33 !
The reason is π is represented in memory by multiple bytes, so the index will skip. This is because iterating over strings iterates over runes and not bytes. Whenever the for-range loop encounters multi-byte rune it converts the UTF-8 representation into 32-bit number and assigns it to the value. The offset is incremented by the number of bytes in the rune. If the for-range encounters a byte that does not represent a valid UTF-8 rune, Unicode replacement character is returned instead.
