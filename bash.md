**`$IFS` and piping `ls` output when filename has space**

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
for f in $(ls *.eml ); do
    cat $i
done
```
 
we can also change it to other things, like `IFS=$','`

==============================
**echo special characters: -e and $'string'**

`echo '\n'` prints literal "\n", not a newline.
use `echo $'\n'` will expand with backslash-escaped cahracters replaced by special characters
or, `echo -e '\n'`, `-e` means escape sequences

==============================
**For loop to operate files**
can directly use 
```basht
for i in *.txt; do
    echo $i
done
```
==============================
