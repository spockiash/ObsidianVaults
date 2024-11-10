To open file with vim use command `vim file.txt`. Vim is exited with `:q` or `:q!`.
# Modes
When file is open we are in normal mode. In normal mode every key has its functionality. For example colon will execute command when enter is pressed.
Writing is done in insert mode. To get into insert mode press letter `I`. To escape insert mode press `esc`. To save the work press `:wq` in the normal mode.
## Normal mode
### Getting into insert mode
There are different ways of getting into insert mode:
* `I` will give insert mode in current line before cursor
* `A` will give insert mode in current line after cursor
* `O` create new line below cursor
* `SHIFT + I` enters insert mode at the beginning of a line
* `SHIFT + A` goes to the end of the line
* `SHIFT + O` creates new line above
### Combined commands
Commands can be combined with line values. For example typing in normal mode number with arrow up/down will move cursor up or down to specific line number defined by input. For example 5 + arrow down will move 5 lines below.
### Navigation
Navigation is done using `hjkl` keys. They mimic arrow keys that can be also used.
### Undo and Redo
To undo changes use key `u` in normal mode. To redo use `CTRL + r`. The undo and redo command can be combined with number for example `3r` will do 3 redo actions.
### Copy and delete line
Lines can be copied with `yy` command and lines can be deleted with `dd`. When pasting lines it includes line breaks.

We can delete only part of the line after cursor by `SHIFT + D`.
### Pasting lines
When using `p` the line will be put below current line and when `P` is used the line will be put above.
When pasting text without new line characters `p` will paste it on current line at the end of the cursor and `P` to place it before cursor.
### Changing line
Changing line means deleting line and entering insert mode at its place. It is done with `cc`.

We can change rest of the line after cursor with `SHIFT + C`.
## Visual mode
Visual mode is accessed in normal mode via `V`. It is used for selecting. In the visual mode the selected text can be deleted with `d` key.

### Copy and paste
To copy selected text in visual mode press `y` for yank. To paste use `p` in normal mode.
# Settings
Settings are configurations for vim. For example we can show line numbers with following command:
```
:set number
```
To enable relative number lines we can use:
```
:set relativenumber
```
We can also enable mouse with:
```
:set mouse=a
```
We can also change `tabstop` and `shiftwidth parameters` and so on.