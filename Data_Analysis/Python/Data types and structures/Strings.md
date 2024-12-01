Strings represent text data, string literals can be written with double or single quotes:
```python
a = 'This is some text'
b = "This is also some text"
```
Python supports multiline string literals:
```python
c = """
This is multiline
text that is on
multiple lines.
"""
```
Under the hood python automatically adds newline symbol, we can get how many new lines there are with `count` method:
```python
c.count("/n") # returns 3
```

Python strings are **immutable** so after we create a string we cannot modify it. If we need to modify string we have to use a method that creates new string such as `replace`:
```python
a = "this is a string"
new_str = a.replace("string", "longer string")
# result this is a longer string
```
After this operation the original string is unmodified.
## Strings as series
String is sequence of Unicode characters and act as [[Lists]] or [[Tuples]]:
```python
s = "python"
list(s) # ['p', 'y', 't', 'h', 'o', 'n']
s[:3] # 'pyt'
```
The syntax [:3] is called slicing and is implemented for many kinds of sequences.
## The escape character
Escape character `\` is used for escaping special symbols. There is also option of using `r` as preface when leading the string:
```python
r"Path\to\file" # r"str" interprets string as is
```
The `r` stands for raw.
## Concatenation
Strings can be concatenated by addition operation:
```python
a = "this is"
b = "string concat"
c = a + b # this is string concat
```

## String formatting
Python has system for string formatting using templates. String object support format method that act on the template:
```python
template = "{0:.2f} {1:s} are worth ETH{2:d}"
template.format(124.12, "BTC", 1)
# '124.12 BTC are worth ETH1'
```
The formatted elements are provided as arguments into the format function and each correspond to the curly bracket specifiers.
The first specifier `{0:.2f}` designates first item with index 0, and the format option `.2f` means floating point number with two decimal places. The other `s` stand for string and `d` is for exact integer.
### f-strings
From python 3.6, they are formatted string literals and are more convenient than formatted strings. They are strings lead with `f` symbol.
```python
a = 15
b = 14.65
c = "meassure"
result = f"{a} is equal to {b} units of {c}"
print(result)
# 15 is equal to 14.65 units of meassure
```
Format specifiers can be added like this `{b:.2f}`.