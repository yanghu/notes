**Registers**

use `:reg` to display registers

previously delete/yanked lines are stored in register 0~9

`"*`:  system clip board

`"%`: file name

use capital letter register name to APPEND to it instead of overwrite

**Docs**

`K` jumps to the man page. for Golang, it jumps to GoDocs.

ctrl+] jumps to tag


**Jumps**

`[{` : jumps to previous bracket"{". useful in C/C++/Golang

`e`: jump to end of current word. (unlike `w`, which jumps to start of next word)

`ge`: jump back to the end of previous word

`*`: search next

`#`: serach previous

`;`: repeat previous `f` command in same direction

`,`: repeat previous `f` command in opposite direction

`Ctrl+^(6)`: Jump to previous file/buffer

`Ctrl+F`: scroll forward one screen

`Ctrl+B`: scroll backward

`Ctrl+D`: down half screen

`Ctrl+U`: up half screen

`H`,`M`,`L`: go to top/middle/bottom of screen. `nH`, `nL` moves to n lines below/above the top/bottom


**Reposition with `Z`**

`z<CR>`: move current line to top of screen

`z.`: move current line to middle

`z-`: move current line to bottom


**Editing**

`J`: join two lines

`r`: replace one character

`s`: substitute (remove current character and go to insert mode)

`C`: change till end of line (like `c$`)

`D`: same as `d$`

`p`: paste AFTER the cursor

`P`: paste BEFORE the cursor (which usually is what we want)

`~`: toggle case

`Ctrl+R`: redo undo

**Windows**

`Ctrl-W, -/+/=` : reduce/increase/equal current windows height by one line

`Ctrl-W, </>` : change width

`Ctrl-W, c`: close window

`Ctrl-W, o`: close all other widows

`zn`: set current window to n lines

`:resize n` : increase/decrease window size to n lines

`:vertical resize n`: resize width to n


**File Explorer (:Ex)**

1. `d` creates a new director
2. `%` creates a new file
3. `D` deletes a directory/file
4. `R` renames a file

========================================
#EX commands
========================================
ex commands consists of a line address plus a command.

`:s` : repeat last substitution. or use **`&`** for the same thing


`:r` : read. append filename, or shell command. example:

```
:r !date    #read current date
:r !sort phone.txt      #read the file, sorted
```

`g/regex/`: get lines. can append other commands. example:

```
:g/^Chapters/t$      #will copy lines starting with "Chapters" to the end of file. (t for copy, $ for last line)
:g/<F\d>/m$         #move all lines containt <F0~9> to the end of file.(example: edit .vimrc and want to check key mappings for F-n keys)
```


**Ctags options**

```
#specify language
ctags -R --languages=PHP .

#exclude files
ctags -R --exclude="*.js" .
```

