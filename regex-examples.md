##1. Use perl to quickly fix files (-n -e)
```bash
#  prepend quote marker at start of line
perl -i.bak -n -e "s/^/|> /g;print" filename

# remove blank lines
perl -i.bak -n -e "print if /\S/" filename

# remove traing spaces
perl -i.bak -pe "s/\s*\n/\n/" filename
```
