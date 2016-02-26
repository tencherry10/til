### Delete all .svn directory

```
find . -iname ".svn" -print0 | xargs -0 rm -r
