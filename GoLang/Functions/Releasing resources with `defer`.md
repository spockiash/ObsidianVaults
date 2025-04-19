The `defer` keyword is paired with functions that handle releasing external resources. For example with reading file, once the file handler is properly establish and the contents are read into memory we can use `defer file.Close()` to ensure the resources are released:
```go
func processFile(fileName string) ([]byte, error) {
    file, err := os.Open(fileName) // Open file
    if err != nil {
        return nil, err
    }
    defer file.Close() // Ensure the file is always closed

    data, err := ioutil.ReadAll(file)
    if err != nil {
        return nil, err
    }
    
    return data, nil
}
```
TODO: study this more when doing more advanced stuff