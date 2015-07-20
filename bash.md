###**`$IFS` and piping `ls` output when filename has space**

when piping output of `ls` to a command that accepts filenames, consider this example

```bash
for i in $( ls *.eml ); do
    cat $i
done
```
 if there are spaces in filenames, like 'my file.eml', it will be treated as two files 'my' and 'file.eml'. The reason is that, for loops split the array using whitespaces. 

 The `$IFS` variable is used by for loops to split the input. therefore we can change it to let it split using something other than white spaces. In this case, we want it to split using "\n\b" 

```bash
SAVEIFS=$IFS
IFS=$(echo -en "\n\b")
for f in $( ls *.eml ); do
    cat $i
done
IFS=$SAVEIFS
```
 
we can also change it to other things, like `IFS=$','`. 

TIP: it's not necessary to change IFS in the previous example, we can use `for i in *.eml` instead of `for i in ( ls *.eml )`.

**More about IFS**

The following code will read the entire input to $line, since `IFS=` sets IFS to null and no word splitting will be done.

Tip: `var=foo command` temporarily override the var for one command

```
while IFS= read -r line
do    
    echo $line
done < /path_to_text_file
```



==============================
###**echo special characters: -e and $'string'**

`echo '\n'` prints literal "\n", not a newline.

use `echo $'\n'` will expand with backslash-escaped cahracters replaced by special characters
or, `echo -e '\n'`, `-e` means escape sequences

==============================
###**For loop to operate files**
can directly use 

```bash
for i in *.txt; do
    echo $i
done
```

==============================
### Command line edit mode| Emacs mode
    - set -o vi (vi mode)
    - set -o emacs (emacs mode)

`^L`: clean screen, move to top

`^V`: quoted insert

`^[`: ESC

`^C`: capitalize word after point

`ESC-U`: change word to all capital after cursor

`ESC-L`: all lower case

==============================
##Writing scripts

### Debuggin bash script 
* with -x option
* use `set -x` and `set +x` to specify parts of the script be debugged. `set -x` will print traces before executing


### Variables

** VARNAME="value" **

only avaiable in current shell. need to use `export VARNAME="value"` to make it avaiable for child process

**_ Special parametes_**

```
$* : expands to positioanl parameters, starting from one. 
$@ : expands to positional parameters. ALWAYS use $@ instead of $*
$# : expands to the total number of positional parameters, in decimal
$? : expands to the exit status of the most recently executed pipeline
$- : expands to the current option flags
$$: expands to the process ID of the shell
$!: expands to the process ID of the most recently executed background command
$0: expands to the name of the shell or shell script
$_: it contains the absolute filename of the shell or script being executed
```

### Quoting characters

* Single quotes: preserve LITERAL value of each character. cannot escape by backslash

* Double quotes: everything preserved except for `$`, backticks(`\``) and backslash

    - backslash can escape $, \`, ", \, and newline. 
    - Dollar sign expands variables

* ANSI-C quoting: $"STRING", backslash-escaped characters are replaced as special characters, like \t, \n, etc.


### Shell Expansion

**Brace expansion**

use comma to separate

```
echo sp{el,il,al}l
>  spell spill spall
```

**Tilde expansion**

If a word begins with an unquoted "~", all of the characters up to the first unquoted slash are considered _tilde-prefix_. if nothing in the _tilde-prefix_ is quoted, the characters in the _tilde-prefix_ following the tilde are treated as a possible login name. 

* if the login name is null, $HOME is used. 
* if login name is not null, the home directory associated with the login name is used
* if the prefix is '+', e.g., '~+', PWD is used.
* if it's '~-', OLDPWD is used
* if it's a number N, e.g., '~N', element from directory stack is used.
* use `dirs -v` (alias `d` in my zshrc) to show history directories with stack index.
* if login name is invalid, word left unchanged. 


```bash
echo ~root    #displays /var/root
echo ~1     #displays previous folder
dirs -v      #show dir history with stack index
cd ~2       # go back to the directory (two steps before)

```

**Parameter expansion**

"$" introduces parameter expansion, command substitution and arithmetic expansion.

parameter name could be enclosed in braces, which are optional, but can protect.

basic form: ${PARAMETER}, the value of PARAMETER is substitued. the brace is required if "PARAMETER" is a positional parameter with more than one digit, or if "PARAMETER" is followed by a character that is not to be interpred as part of its name

if the first character of "PARAMETER" is "!", like, ${!AAA}, bash uses the value of the variable formed from the rest of the name ("AAA" here) as the name of the variable; then it is expaneded. called _indirect expansion_


```bash
GREETING=HELLO
HELLO=howdy
echo ${!GREETING}  # will show : howdy
```


`${VAR:=value}` allows for creation of the variable if not exists.

**Command substitution**

$(command) or use backstick: `command`. it use the standard output of the command, with any trailing new lines deleted. 

when using backstick, backslash can be used to escape "$", "\`" or "\". when using "$(command)", nothing is escaped


**Arithmetic expansion**

$(( EXPRESSION ))

expression is treated as if it were within double quotes. all tokens undergo parameter expansion, command substitution, and quote removal. fixed-width integers. 

shell variables are allowed. within the expression, variables may also be referenced by name without "$" prefix

$[ expression ] is preferred


**Word splitting**

for parameter expansion/command expaions/arithmetic expansion that did NOT occur within double quotes, word splitting is performed.

treats $IFS as delimiter, split the results into words. 

if no expansion, no splitting is perfored.


**File name expansion**

After word splitting, bash scans each word for "\*", "?" and "[".  if any is found, the word is treated as a pattern, and filenames are used to replace it. (alphabetically sorted list of filenames matching the pattern)


**shell options**

use `set -o` to view all options


========================================
##Regex and grep

`grep pattern filename`

single quotes: all literal.

double quote: escape special characters 


**pattern matching without grep**

```
ls -ld [a-c]*       # files starting with a,b,c
```


## GNU sed stream editor

stream editor, does not change original input. can be saved to file by output redirection

can filter text from pipeline feed.
