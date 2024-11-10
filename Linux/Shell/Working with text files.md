Text files can be listed using `cat` command followed by name. For example:
```sh
cat alice.txt #lists the whole text file
cat alice.txt #lists the whole text file
```
To view content of a text file screen by screen use command `less`.  Less files can be navigated with:
* `B` - go down
* `SPACE` - go up
* `/` - Search
* `Q` - Exit

> [!tip] Use command `reset` when binary files mess up the terminal
# Text editors
## Nano
Nano is an lightweight editor. To exit nano use `CTRL+Q`. To save use `CTRL+O`. It is really easy.
## Vi
This is not as easy to use but together with `Vim` this can be powerful editing tool. It uses modes and each mode changes behavior  of the editor.
Basics of use is use `esc` to enter command mode. Then use command `:q` to quit. Use command `:w` to write changes and `:wq` to write and exit the editor. Use `:q!` to exit without changes.