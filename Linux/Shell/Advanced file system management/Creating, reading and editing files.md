Directories can be created by `mkdir` command that can take arbitrary number of arguments:
```sh
mkdir a b # creates two directories inside current working directory
```
To create file we can use touch command:
```sh
touch file1 file2 # creates two files
```
If file of any of the name provide matches already existing file in location, then touch will update the modification time of the file.
To remove a file we can use `rm` command and to remove directory we use `rmdir:
```sh
rm file2
rmdir directory1
```
When using `rmdir` command on an non empty directory the command will fail. To remove directory with files in it we need to delete it recursively using `-r` option:
```sh
rm -r a
```

> [!tip] Use `rmdir` to safely remove empty folders
> Because `rmdir` will not touch without recursion full folders, we can use this to safely clean empty folders from file system.



