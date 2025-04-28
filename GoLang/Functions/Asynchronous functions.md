To execute function asynchronously go does not use classical `async await` syntax found in other programming languages like C# or Python. Instead `go` uses `go` routines. The keyword is `go` before function `f()` when we call it:
```go
func main() {
	go checkUrl()
}

func checkUrl() {
	...
}
```
