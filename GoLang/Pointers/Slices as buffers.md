In most languages when dealing with buffered input like reading external resources from a file or network connection the code looks like this:
```c
r = open_resource()
	while r.has_data() {
		data_chunk = r.next_chunk()
		process(data_chunk)
}
close(r)
```
This pattern has to allocate new memory per each cycle. In Go we can leverage the property of slices not being able to change its length when passed into a function. This avoids more allocations because slice of bytes is created once and then used as a buffer to read data from source:
```go
file, err := os.Open(fileName)
if err != nil {
	return err
}

defer file.Close()
data := make([]byte, 100)
for {
	count, err := file.Read(data)
	process(data[:count])
	...
}
```
The contents of the slice when passed into a function can be changed only up to a length of the original slice.