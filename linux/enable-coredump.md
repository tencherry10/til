### Enabling Coredump

By default core dump is disabled for security reasons. 

If you want the actual core dump file to be written, enable it via ulimit:

```sh
$ ulimit -c unlimited
```

Also in newer versions of Ubuntu, Crashdump may be piped into apport crash reporting/analysis system. 

Look inside ```/proc/sys/kernel/core_pattern``` to see what program gets executed when coredump is triggered.


