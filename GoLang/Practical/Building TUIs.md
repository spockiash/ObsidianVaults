# Tcell and Tview
Tview is built on Tcell. Tcell is an low level package for building TUIs. To install it run in your project:
```sh
go get github.com/rivo/tview@master
```
This installs to the project Tview and related dependencies like Tcell.
## Capturing input
Tview allows for global and local capturing of key events. Most of the time the capture is done on component level utilizing the function `SetInputCapture()`.  It takes function as an argument that can be customized:
```go
textView.SetInputCapture(func(event *tcell.EventKey) *tcell.EventKey {
	if event.Rune() == 'w' {
		return tcell.NewEventKey(tcell.KeyRune, 'j', tcell.ModNone)
	}
	return event
})
```
Or we can customize it further and intercept any key:
```go
textView.SetInputCapture(func(event *tcell.EventKey) *tcell.EventKey {
	if event.Key() == tcell.KeyEscape {
		textView.Clear()
		return nil
	}
	return event
})
```
More information [here](https://github.com/rivo/tview/wiki/CustomKeys).

