**remove old mode new mode changes**

http://stackoverflow.com/questions/1257592/how-do-i-remove-files-saying-old-mode-100755-new-mode-100644-from-unstaged-cha

Sometimes git status will show uncommited changes of files, with the only difference being mode, like

```
diff --git a/.gitignore b/.gitignore
old mode 100644
new mode 100755
```

This can be removed by 

```
git config core.filemode false
```

