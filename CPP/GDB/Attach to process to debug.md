# How to Debug a binary?

## Start binary with gdb
So if you are running your code by:

```c
$ executablefile arg1 arg2 arg3 
```

Debug it on `gdb` by:

```c
$ gdb executablefile  
(gdb) r arg1 arg2 arg3
```

## Add breakpoints
[gdb QuickStart](https://web.eecs.umich.edu/~sugih/pointers/gdbQS.html#:~:text=Type%20%22gdb%20%5Bfilename%5D%22,them%20with%20%22set%20args%22.)

1. **Setting breakpoints** A breakpoint is like a stop sign in your code -- whenever gdb gets to a breakpoint it halts execution of your program and allows you to examine it. To set breakpoints, type "break [filename]:[linenumber]". For example, if you wanted to set a breakpoint at line 55 of main.cpp, you would type "break main.cpp:55".  
      
    You can also set breakpoints on function names. To do this, just type "break [functionname]". gdb will stop your program just before that function is called. Breakpoints stay set when your program ends, so you do not have to reset them unless you quit gdb and restart it.  
      
    
2. **Working with breakpoints**
    
    - To list current breakpoints: "info break"
    - To delete a breakpoint: "del [breakpointnumber]"
    - To temporarily disable a breakpoint: "dis [breakpointnumber]"
    - To enable a breakpoint: "en [breakpointnumber]"
    - To ignore a breakpoint until it has been crossed x times:"ignore [breakpointnumber] [x]"
    
      
    
3. **Examining data** When your program is stopped you can examine or set the value of any variable. To examine a variable, type "print [variablename]". To set the value of a variable, type "set [variablename]=[valuetoset]".

## Save gdb History

[Source](https://www.ece.villanova.edu/VECR/doc/gdb/Command-History.html#:~:text=Set%20the%20name%20of%20the,command%20editing%20characters%20listed%20below.)
(gdb) set history filename /mnt/c/wsl/OS/flexCentOS/flexsys/gdb_history
(gdb) set history save
(gdb) set history save on

