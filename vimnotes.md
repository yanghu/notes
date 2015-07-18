**Registers**

use `:reg` to display registers
previously delete/yanked lines are stored in register 0~9

`"*`:  system clip board
`"%`: file name

**Docs**

`K` jumps to the man page. for Golang, it jumps to GoDocs.
ctrl+] jumps to tage


**Jumps**

`[{` : jumps to previous bracket"{". useful in C/C++/Golang
`e`: jump to end of current word. (unlike `w`, which jumps to start of next word)
`ge`: jump back to the end of previous word
`*`: search next
`#`: serach previous

`Ctrl+F`: scroll forward one screen
`Ctrl+B`: scroll backward
`Ctrl+D`: down half screen
`Ctrl+U`: up half screen
`H`,`M`,`L`: go to top/middle/bottom of screen

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

