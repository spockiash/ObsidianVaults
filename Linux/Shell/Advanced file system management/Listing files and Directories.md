UNIX file system is represented as upside down tree. The base of the file system is called the root and is represented by `/`. From the root there are multiple branches for example `/bin` that holds programs. Then there is `/etc` for configuration files. `/home` for the user directories and others.

Basic navigation is done using `cd` command and `pwd` command will list current working directory.
The home directory is represented using `~`. To get to home directory we can use `cd` command with no arguments. To go into previous directory we can use `cd -`. The hyphen will get us to previous working directory.

Every directory will contain two files `.` and `..`. These are used when navigating using `cd` command. For example `cd ..` will get you one level up in the tree.
## Basic sorting
With `ls` command we have some sorting options:
```sh
ls -lt #sort by modified time
ls -ltr #reverse
ls -lS # sort by size
```
# Types of files
In UNIX-like system everything is a file. Even directory is a file. Therefore we can have the following file types
* Directories
* Regular files
* Executable files
* Links - pointers to other files
* Device files - represent devices
The `dev` directory contains lot of device files. The file can have more detailed type for example device files can have marking of" `crw-rw-rw-   1 root root        1,   5 19. čen 11.10 zero`.
The `c` stands for character device file, that accept stream of characters. `B` would be block file for random access.
UNIX also accepts sockets, doors and named pipe files. Pipe files are also called `FIFOs` meaning first in first out.
# Pattern matching
Also known as globbing or in Z Shell it is known as Filename generation. Pattern matching is done using [[Bash and Z Shell overview#Wildcards|wildcard]]. Special symbol like `*` that enables pattern matching.
Pattern matching is done on the Bash level and the actual command is not aware of this. The command receives all the files.
When Bash cannot complete the pattern (no such file exists) then the command will receive the full name with the special character:
```sh
echo U* #no such file exists
U* #echo the command
```

Z Shell gives error message when pattern cannot be completed. Even when passed with valid parameters together with invalid ones like this:
```sh
echo D* U*
```
## Selecting sequences
When selecting special sequence of a character we can use special character `?`. This way we can match for example any file that contains extension:
```sh
ls *.?*
```
The `?` matches single character.
If we want to select all three letter extension we can use `ls *.???`.

### Selecting range
We can use brackets to specify range of characters to match:
```sh
ls [abc]* #matches all files that start with `a`, `b` or `c`
```
We can do more advanced selection with ranges. For example we can select all characters starting with Uppercase and ending with lowercase using whole range using hyphen character. This way we do not need to specify whole range:
```sh
ls [AZ]*[az]
```
We can do this with numbers as well. For example if we have multiple files with same name but different number at the end:
```sh
ls file[1-4]* #searches for file ending with number like `file3` or `file1`
```
We can combine ranges with specified characters:
```sh
ls [A-Eabc]* # find files starting with A-E range and `a`,`b` or `c`
```
#### Negating pattern
We can use `^` character to reverse the pattern. Now the logical value is flipped so everything specified will not be shown:
```sh
ls [^A-Eabc]* #A-E range and `abc` pattern will be excluded here
```
#### Selecting multiple patterns
To select multiple patterns for example select multiple files that start with letter `m` or `n` and have extensions `.jpg`, `.mp4` and `.png` we can use parentheses like this:
```sh
ls [mn]*(jpg|mp4|png)
```
This way we do not need to specify the pattern for each extension.

We can use extended globbing with `@` character. Bash has this feature disabled by default so to enable it we use:
```sh
shopt -s extglob
```
##### Special modifiers
These work with 
We can use special modifiers inside parentheses to display only certain types of files:
```sh
ls -ld *(.) # displays only regular files
ls -ld *(/) # displays only directories
ls -ld *(@) # displays only symbolic links
```
We can also use this to specify files with only size bigger then 2 kilobytes for example:
```sh
ls -ldh *(LK+2)
```
The symbols have following meaning:
* `L` is qualifier that tells to look for filesize
* `K` mean kilobytes
* `+2` means larger then 2 kilobytes
# Locating files
Most basic way of finding file is done using `find` command. First argument is root folder for the search. Then we need name option `-name` followed by the filename argument. For example we can search for file called `grades2020.csv` somewhere inside home folder:
```sh
find ~ -name grades.csv # finds in home directory file named grades
```
We can do more advanced stuff with pattern matching. Pattern matching must be in quotes so 'grade*' as a name will work:
```sh
find ~ -name 'grades*' # will find files that start with `grades`
```
We can even specify type of a file using `-type` option.
Lets say we want to find pictures and videos inside a directory. To find multiple parameters we need to space out the names with `or`:
```sh
find ~ -name `*.mp4` -or -name '*.jpg'
```
Z Shell offers advanced finding option using two asterisks with ls command:
```sh
ls **/*(jpg|mp4)
```
After the slash the pattern will be matched.