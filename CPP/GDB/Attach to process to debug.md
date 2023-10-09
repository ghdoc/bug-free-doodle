# How to Debug a binary?
1. So if you are running your code by:

```c
$ executablefile arg1 arg2 arg3 
```

Debug it on `gdb` by:

```c
$ gdb executablefile  
(gdb) r arg1 arg2 arg3
