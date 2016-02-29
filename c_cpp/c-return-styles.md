## Overview of C error handling / return style

1. Return function output via a reference parameter and return status normally through the stack

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

1. Return output via stack and the error code via a reference argument

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
    
1. Use special sentinel values. Lots of C library functions work this way. For e.g. getc() which return EOF when there is an error. Zero can be a sentinel for ptr returns. Negative values could be used as a sentinel for unsigned value output.

  PRO
  
    1. Lots of C library function is like this.
    
  CON
  
    1. Not always possibly to have a sentinel value
    1. Even if you have a sentinel value, you may not be able to express all the error condition. 
      If you need to differentiate between different error conditions. Then you still have to do some version of above or use an out of channel error system like errno.
      

    
    
    
    

   

