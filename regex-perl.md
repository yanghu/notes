2015-07-16 10:36am

## Command line options
-p: Places a printing loop around your command so that it acts on each line of standard input. It overrides the -n switch 

-e: Allows you to provide the program as an argument rather than in a file. You don't want to have to create a script file for every little Perl one-liner.

-n: automatically loops over the lines. 

-i: Modifies your input file in-place (making a backup of the original). Handy to modify files without the {copy, delete-original, rename} process.

-w: Activates some warnings. Any good Perl coder will use this.

-d: Runs under the Perl debugger. For debugging your Perl code, obviously.

-t: Treats certain "tainted" (dubious) code as warnings (proper taint mode will error on this dubious code). Used to beef up Perl security, especially when running code for other users, such as setuid scripts or web stuff.

Examples:
```bash
    perl -i.bak -pe "s/^/>| /g" filename
```

### Basics
```perl
$var =~ m/regex/    #attempt to match the given regex to the text in the variable `$var` 
m/regex/            # does the match operation on default variable `$_`, which is the line read from file
s/regex/replacement/    # does match and replace.
s/regex/replace/i   #case insensitive match and replace

```

### Modifiers
Different modes 

    * /i: case insensitive
    * /m: multiline mode (`^` and `$` matches line start/end instead of start/end of whole string)
    * /s: dot matches all mode
    * /x: free-spacing and comments mode.(spaces and comments are ignored)
    * /o: compile only once

**Dot matches all mode(single-line mode)**

dots typically doesn't match new lines. so `.*` only matches the rest of the line. If it's a multiline string, `/s` mode will allow `.*` to match anything, including new lines. so `.*` becomes "rest of the content".

**Enhanced line-anchor mode, a.k.a, "multiline mode" `/m`**

`^` and `$` originally only matches the start and end of the whole string, and they does NOT match embedded newlines. In this mode, `^` and `$` matches the embedded newlines.

Note that, `\A` and `\Z` can be used in this mode to achieve the original effect, e.g., match start/end of the whole string.



### Flavor and dialect
    * non capturing: (?:regex)
    * lookahead: (?=regex)
    * lookbehind: (?<=)

## Perl file reading
**read mode(chunk mode)**

    * `$/` determins where the chunk ends when using `<>` to read a line from file.
    * `<>` operator gives next line of input WHEN you assign from it to a `$variable`. When reach EOF, it  returns false
    * a default variable is used (assigned the value of `<>` and being used as the target string)

```perl
while ($line=<>) {
    # work with line here
    if ($line =~ m/^\s*$/){     # see if we have an empty line
        last;     # break out of while loop
    }
}

# process for the rest of messages here
while (<>){
    #work with rest
    if (s/name\s*=\s*(\w*)$/$1 is my name/i){
        print
    }
}
```


## Default parameters

###  `$_` : The default parameter. 

if no variable is specified, the line read in is saved to `$_`. 

### `$.` : Line number

