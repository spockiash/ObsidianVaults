# Command glossary
```sh
# commands
pwd - # print working directory
ls - # list contents of directory


```
Most basic
# Navigating File system
Directories are navigated using `cd` command with arguments that tells the command where to change the directory to. Along with arguments we have options that start with `-` for example to show hidden directories we can use list command with option `-a`:
```sh
ls -a # shows all
```
We can show more information by using `-l` option. The options can be combined for example with:
```sh
ls -l -a # shows hidden files in long format
```

To show what type a file is, we can use command `file` because extensions are optional.
# Naming conventions
Linux file system is case sensitive. Linux file system by default does work with spaces in file names. When using paths with file that has spaces in it we can use single parentheses to quote it as argument or we can use `\` character that disables space meaning in this context:
```sh
cat 'file name with spaces.txt' #passed as argument
cat file\ name\ with\ spaces.txt #the same as above
```
When the name is passed to the terminal accidentally without the quote complete, the terminal will actually wait for second part of the character stream even with enter key. This would be bad so exit using `ctrl + C`.

File name can be white space and then would show up as `?`. To create a whitespace file we can do:
```sh
touch `
`
```
Some characters have special meaning and touch will not work with them for example `$`. We can actually use backspace or quotes to escape the character:
```sh
touch \$file
```
