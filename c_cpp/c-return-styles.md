## Overview of C error handling / return style


#### Return function output via a reference parameter and return status normally through the stack

```c
int foo(int * out, int in1, int in2);
```

PRO

  1. easy to execute / check for error at the same time

  ```c
  if( foo(&out, in1, in2) != SUCCESS) {
    // handle error
  }
  // use out here
  ```

CON

  1. Can't daisy chain result. For e.g. `bar(foo(in1, in2), in3, in4)`
  1. Can be annoying if the user of code knows it is not possible to fail
  1. If you have to handle different errors differently (with multiple if cases), it may still be ugly

#### Return output via stack and the error code via a reference argument

```c
int foo(int * ok, int in1, int in2);
```

PRO

  1. More intuitive, function returns result not status
  1. Can possibly chain results if you can gaurantee function can't fail (possible with well formatted inputs)

CON

  1. Possibly annoying to use
  
  ```c
  int ok;
  int out = foo(&ok, in1, in2);
  if( ok != SUCCESS ) {
    // handle error
  }
  // use out safely here
  ```
    
#### Use special sentinel values. Lots of C library functions work this way. For e.g. getc() which return EOF when there is an error. Zero can be a sentinel for ptr returns. Negative values could be used as a sentinel for unsigned value output.

PRO

  1. Minimal number of arguments but possibly harder to use
  
  ```c
  int c;
  FILE * fp = fopen("file.txt", "r");
  if( (c == fgetc(fp)) == EOF) {
    // could be EOF or could be error (must check)
    if( ferror(fp) ) {
      // handle error
    } else {
      // got EOF ==> wrap up 
    }
  }
  ```
  
  1. Lots of C library function is like this.
  
CON

  1. Not always possibly to have a sentinel value
  1. Even if you have a sentinel value, you may not be able to express all the error condition. 
    If you need to differentiate between different error conditions. Then you still have to do some version of above or use an out of channel error system like errno.
    
#### Use an out-of-band error reporting system (like errno).

PRO

  1. Function Call looks simpler
  
  ```c
  unsigned long ul; 
  errno = 0;
  if( (ul = strtoul (buffer, NULL, 0)) == 0) {
    if(errno != 0) {
      // handle error
      
    }
    // else it is actually 0
  }
  // use ul here
  ```
  
CON

  1. out-of-band error reporting will have global state. So, it will be problematic for multi-threaded programs.
  1. problematic for library functions b/c you may have nested calls which wants to report error via errno
  

