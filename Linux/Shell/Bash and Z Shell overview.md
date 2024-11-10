Shells are ways of interacting with a UNIX system. They provide interface for human user and other programs allowing it to control some system.
On UNIX systems there are many popular shells, most popular are Bash and Z Shell.

Bash and Z Shell are very similar. Z Shell provides more customization from Bash.

Here is typical shell prompt:
`user@system-name:~$`
The dollar sign means the shell is ready for input.

Users typically interact with shell via terminal emulator. The terminal emulator supports fonts and colors and interacts with the shell via control codes. It translates user input for the shell.

The prompt tells user the shell is ready to take command. It usually starts with user name and host name. It can be customized.

Using tab key, in bash will complete with any valid command that starts with the sequence. In Z Shell this will give menu of all the different options.

Bash features:
* Up and down arrows recall commands (or ctrl-p or ctrl-n)
## Manuals
Unix systems have manual pages system. To view manuals use command `man <command name>`.
Manual pages are navigated using `space` and `b` key to move up or down.
Manuals can be searched using `/` key.
## Commands, arguments and options
Commands are programs, routines or scripts accessible via shell. For example `ls` is command for listing content of directory. Arguments is any data that is passed to the command. Options are special arguments that start with `-` and they modify how the command behaves.
## Using Vi
Vi is program for editing text. It uses modes and default mode is command mode that accepts commands. To write text we can use `I` and to exit insert mode press `esc`. 
## Becoming a Power User
### Pipes and Redirection
Pipes are used to pass output of a program or command into another. To use pipe we use symbol `|` like this:
```sh
ls | less #pipes ouput of ls command into less. Now the list of large directory can be listed
```
We can do more advanced stuff for example sort things from grep. For example we can find records in `tsv` table `oilrigs_list.tsv` and pass it into sort to get sorted findings from files:
```sh
grep Mexico oilrigs_list.tsv | sort
```
The output of the pipe can be redirected into file using `>` symbol for example:
```sh
grep Mexico oilrigs_list.tsv | sort > sorted_mexico_drills.txt
```
But this will override any files that already exists with specified name.
We can use more advanced stuff for example get only specific column using command `cut -f`:
```sh
cut -f  oilrigs_list.tsv # gets only depth column
```
We can then chain it with grep using pipe to get for example only rigs with depth of `7000`:
```sh
cut -f 1 oilrigs_list.tsv | grep 7000 
```
We can then count the number of stations in certain depth using `wc` command standing for word count:
```sh
cut -f 1 oilrigs_list.tsv | grep 7000 | wc -l #count lines
```
### Wildcards
[[Listing files and Directories#Pattern matching|Wildcard]] is represented using `*` symbol and it is symbol for all the file in a directory. For example when used with `grep` like `grep tiny *` it will find  in all file lines that have sequence of letters `tiny` in the current working directory.

We can use it with `echo` to echo content of current directory:
```sh
echo * # lists file names
```
We can combine it with ls and for example find all files ending with an `a` we can do:\
```sh
ls *a #shows files ending with a
```
To find file containing sequence of characters use `ls *a*`. We can even leverage patterns using wildcards to sort files into directories based on their file name:
```sh
mkdir pictures text
mv *txt text #use wildcard pattern to move all text files into text dir
mv *jpg pictures
```
### Custom commands
To run custom commands stored in `bin` folder run the following:
```sh
export PATH=$PATH:~/bin
```
On bash we can use `.profile` or `.bashrc` for interactive shell to customize behaviour. On Z shell it is `.zshenv` or `.zshrc` file.