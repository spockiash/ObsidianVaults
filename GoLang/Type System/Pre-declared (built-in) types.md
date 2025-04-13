Go has many so called predeclared types. They are similar to types found in other languages like booleans and integers. By default Go assigns declared variables so called `zero value` that is declared but not assigned any value.
## Literals
Go has support for literals like any other language. Literals are considered untyped.
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
## Booleans
Booleans represent binary state `true` or `false`. The default zero value is false:
```go
var flag bool // no value assigned, set to false
var isAwesome = true
```
