The `if` statement works just like every other language, the only difference is the condition is not in parentheses:
```go
n := rand.Intn(10)
if n == 0 {
	fmt.Println("That's too low")
} else if n > 5 {
	fmt.Println("That's too big:", n)
} else {
	fmt.Println("That's a good number:", n)
}
```
Go allows to scope a variable specific for an if statement:
```go
if n := rand.Intn(10); n == 0 {
	fmt.Println("That's too low")
} else if n > 5 {
	fmt.Println("That's too big:", n)
} else {
	fmt.Println("That's a good number:", n)
}
```

This way the variable needed for the operation is limited just to the code block itself, making cleaner code.