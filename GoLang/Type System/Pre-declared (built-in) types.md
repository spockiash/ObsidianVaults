Go has many so called predeclared types. They are similar to types found in other languages like booleans and integers. By default Go assigns declared variables so called `zero value` that is declared but not assigned any value.
## Literals
Go has support for literals like any other language. Literals are considered untyped. This means we can assign any numeric literal to any numeric type:
```go
var x float64 = 10
var y float64 = 200.3 * 5
```
We however cannot assign string literal type to numeric and vice versa. If we would try to assign larger value to smaller type, we would get compile-time error.
### Integer literal
By default integer literals are sequence of numbers with base 10 by default. Similar to C we can use prefixes to indicate other bases like `0b` for binary, `0o` for octal and `0x` for hexadecimal. Go supports either upper and lower case prefix. Leading zero in integer integral can also indicate octal value.

To improve readability we can add underscores `_` between the number to separate thousands in the value. It cannot be placed as leading character. It can be used in other base numbers to improve readability of bytes.
### Floating point literal
Floating point literals use decimal point to indicate the fractional portion. They also have exponent with the letter `e` and positive or negative number: `6.03e23`. Hexadecimal float literals use exponent as letter `p` and the exponent value is in base 10.
### Rune literals
Rune literal represents character and is surrounded by single quotes. Single and double quotes are NOT interchangeable in go. Rune literals can be written as single Unicode characters `('a')`.

Rune literals also support 8-bit octal numbers `'\141'`, hexadecimals as `'\x61`. 16-bit hex numbers as `'\u0061'` or 32-bit Unicode numbers `'\U00000061'`.

Rune literals can be escaped to create special values like new line `'\n'` and others.

Octal values are useful for representing POSIX permission flags like` '0o777'` meaning `rwxrwxrwx`.
### String literals
There are two ways of indicating string literals. Most of the time, you should use double quotes to created an interpreted string literal: `"Hello, world"`. These strings interpret rune literals (both numeric and backslash escaped) into characters.

> [!info]
> You cannot use backslash to escape single quote inside a single quoted string

Unescaped backslashes, newlines and double quotes are the only illegal things in interpreted string.
#### Raw string literals
Raw string literals provide easier way to create string literals without the need for escaping special characters. Raw literals use back-quotes:
```go
`Greetings and
"Salutations"`
```
The literals can be written across multiple lines as well.
## Type conversions
More about type conversions [[Type conversions| here]].
## Booleans
Booleans represent binary state `true` or `false`. The default zero value is false:
```go
var flag bool // no value assigned, set to false
var isAwesome = true
```
## Numeric types
Go supports 12 numeric types. Integer types (signed and unsigned), float types and also complex types.
### Integer types
Go has multiple sized integers both signed and unsigned:
* `int8` 
* `int16`
* `int32`
* `int64`
* `uint8`
* `uint16`
* `uint32`
* `uint64`
Integers can have special names, for example `byte` is alias for `uint8`. There is also `int` alias that is either signed 32-bit or 64-bit based on CPU bit size. Unlike `byte` it is illegal to perform operations between `int` and `int32` or `int64`. Integer literals default to being of `int` type.

>[!info]
>Some 64-bit CPUs use 32-bit signed integer for the `int` type.

There is also `uint` alias for the unsigned 32-bit. It has same rules as `int`.
#### Integer operations
Go provides basic operators like addition, multiplication and modulo just like other languages. Arithmetic operators can be used with `=` to modify a variable:
`+=, -=, *=, /= and %=`:
```go
var x int = 10
x *= 2 //x will be 20
```
Integers can be compared with operators:
`==, !=, >, >=, < and <=`
Go also has bit-manipulation operators for integers. You can shift left and right with << and >>, or do bit masks with & (bitwise AND), | (bitwise OR), ^ (bitwise XOR) and &^ (bitwise AND NOT). As with the arithmetic operators, you can also combine all bitwise operators with `=` to modify a variable.

### Floating-point types
Go has out of the box `float32` and `float64`. Go uses by default the `float64` option. Floating-point numbers can have large values but are not exact. This means floating point numbers are limited to applications where inexact value is no matter or the limitations are well understood.

Floating-point number cannot represent decimal value directly. In such cases where precision is needed third-party [[Modules and Packages|modules]] must be used.
#### Operations on floating-point numbers
All operations are legal except modulo `%`. When we divide non-zero value by zero we get either `+Inf` or `-Inf` (infinity). Dividing `0` by `0` will result in `NaN` (Not a Number).

One caveat of float types is the inability to use direct comparison with operators like `==` or `!=` because of the inaccuracy problem of floats. More information about proper comparison can be found [here](https://floating-point-gui.de/errors/comparison/).
### Complex types
Go has complex types. But I am skipping it, because they are not useful unless one wants to do math stuff.
### Strings and runes
Strings are built-in type in go. They can be operated on by comparison operators `==` or `!=`, or ordering with `>`, `>=`, `<` and `<=`. They can be concatenated with `+` operator.

Go strings are immutable, you can reassign the value of a string variable, but you cannot change the value of the string that is assigned to it.
#### Rune
Go has `rune` type that is actually alias for `int32`. It is used to represent characters.