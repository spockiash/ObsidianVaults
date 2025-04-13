Most languages have automatic type conversions. But these come with special rules and can produce unexpected results. Go allows only for explicit conversions:
```go
var x int = 10
var y float64 = 30.2
var sum1 float64 = float64(x) + y
var sum2 int = x + int(y)
```
This strictness in explicit type conversions comes with some limitations, for example we cannot use other types as `boolean` like in C for example. Go therefore does not allow for "truthy" values