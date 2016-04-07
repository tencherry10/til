### Enabling Coredump

By default core dump is disabled for security reasons. 

If you want the actual core dump file to be written, enable it via ulimit:

```sh
$ ulimit -c unlimited
```
