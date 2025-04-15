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
