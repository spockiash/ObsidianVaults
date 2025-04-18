# Expression switch
An expression switch is a statement that evaluates some expression. It evaluates the expression based on internal comparison, therefore the switching expression must be done with comparable types. Also the types cannot mismatch.

The expression does not need to evaluate to boolean type.
```go
x := 2
switch x {
case 1:
	fmnt.Println("one")
case 2:
	fmt.Println("two")
default:
	fmt.Println("other")
}
```
* The expression can be of any type
* Each case must be a value that is comparable to the expression
* Go uses internal `==` to handle each case
* Types must be comparable
The variable can also be declared scoped same as `if` statement:
```go
switch x:= 2; x {
	//....
}
```
Go does not require break statement, because it automatically adds it to every case. By default fall-through is not working. To trigger multiple matches per case go allows to add multiple values per case:
```go
case 1, 2, 2, 4:
```
Unlike other languages, the cases does not need to be literal but variables can be used. Go also allows for empty case. Go also provides the `fallthrough` keyword to allow classic switch behavior.

The `break` statement can be used in cases to exit the case early. When dealing with switch statements in a loop, we can use breaks with labeled loops to break out of the loop:
```go
loop:
	for i := 0; i < 10; i++ {
		switch i {
		case 0, 2, 4, 6:
			fmt.Println(i, "is even")
		case 3:
			fmt.Println(i, "is divisible by 3 but not 2")
		case 7:
			fmt.Println("exit the loop!")
		break loop
		default:
			fmt.Println(i, "is boring")
		}
	}
```
With this setup, it will break out of the loop once 7 is encountered in the switch. If the loop label was omitted, it would simply break out of the case.
## Blank switches
When the expression is left out from the switch statement, it can become flexible tool. Each case can be provided with expression of equality and this can be used as some sort of if statement.
```go
words := []string{"hi", "salutations", "hello"}
for _, word := range words {
	switch wordLen := len(word); {
	case wordLen < 5:
		fmt.Println(word, "is a short word!")
	case wordLen > 10:
		fmt.Println(word, "is a long word!")
	default:
		fmt.Println(word, "is exactly the right length.")
	}
}
```
