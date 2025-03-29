# Package
Every Go program is made up of packages. Program starts running in package `main`, the program is using some packages with import paths for example `fmt` and `math/rand`:
```go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite number is", rand.Intn(10))
}
```
By convention the package name is the same as the last element in the import path. For example the `math/rand` package has files that begin with statement `package rand`.

Package can also be taught of as collection of files in a folder.
# Module
Module is collection of packages and are building blocks for Go projects. Its main goal is to simplify dependence management.
## Setting up a Go Module
First we need to create a new directory as a root of the module. Then we use command `go mod init <module_name>`. This creates file `go.mod`:
```
module my-go-project
go 1.16
require (
    github.com/go-sql-driver/mysql v1.5.0
)
```
