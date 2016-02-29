## Overview of C error handling / return style

1. Return function output via reference and return status normally through the stack

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

