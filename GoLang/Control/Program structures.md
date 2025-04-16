# Blocks
The most basic composition structure of Go program is a block. Block is any code segment where variables, types, constants, functions and so on are declared. Go differentiates between the location for the blocks. For example code in packages is in package block. When dealing with import statements, they are relevant to file blocks in the imported files and so on. Function blocks and so on.
# Shadowing Variables
Shadowing occurs when we have a variable in outer scope and then we declare variable with the same name in an inner scope:
```go
func main() {
	x := 10
	if x > 5 {
		fmt.Println(x) // 10
		x := 5
		fmt.Println(x) // 5
	}
	fmt.Println(x) // 10
}
```

# Control structures
* [[If statements]]
* [[Loops]]