
## Overview of C error handling / return style

1. [Output via reference argument](#return-output-via-a-reference-argument)
1. [Error via reference argument](#return-error-via-a-reference-argument)
1. [Special Sentinel Values](#use-special-sentinel-values)
1. [Out-of-band error system](#out-of-band-error-reporting-system)
1. [Return struct with error info](#return-struct)
1. [Macro based try-except](#macro-based-try-except)
1. [Error string based](#error-string-based)

---

#### Return output via a reference argument

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

#### Return error via a reference argument

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
    
#### Use special sentinel values

PRO

1. Some returns have natural sentinel values. Zero can be a sentinel for ptr returns. Negative values could be used as a sentinel for unsigned value output (like lengths).
1. Lots of C library function is like this, so C programmers are familiar. For e.g. fgetc(). 
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

CON

1. Not always possibly to have a sentinel value
1. Even if you have a sentinel value, you may not be able to express all the error condition. 
  If you need to differentiate between different error conditions. Then you still have to do some version of above or use an out of channel error system like errno.
  
#### Out-of-band error reporting system

PRO

1. Common among C / Linux standard library. (look up errno)
1. Function call looks simpler

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

#### Return struct

PRO

1. No global state
1. Easy to add additional error information (like a string to explain error, or even a stack trace!)
1. Unambiguous intent

```c
typedef struct {
  int ret;
  int err;
} int_ret_t;

int_ret_t foo(int in1, int in2);

int_ret_t r;
if( (r = foo(1,2)).err != SUCCESS) {
  // handle err
}
// use r.ret here
```

CON

1. Extremely heavy-weight (possibly lots of structs or have to use void * and memory)
1. Requires using to include header file about struct

#### Macro-based try-except

Abuse setjmp/longjmp Here is a simplified explanation. C Interface and Implementation book has a more sophisticated (but more complicated) version.

```c
#include <stdio.h>
#include <setjmp.h>

#define TRY do{ jmp_buf ex_buf__; int err = 0; if( (err = setjmp(ex_buf__)) == 0){
#define CATCH } else {
#define ETRY } }while(0)
#define THROW(x) longjmp(ex_buf__, x)

int main(void) {
  TRY {
    printf("In Try Statement\n");
    THROW(1);
    printf("I do not appear\n");
  } CATCH {
    switch(err) {
    case  1: printf("Got Exception 1!\n"); break;
    case  2: printf("Got Exception 2!\n"); break;
    default: printf("Got unknown Exception!\n"); break;
    }
  }
  ETRY;
  return 0;
}
```

PRO

  1. Familiar try-except to most other "higher level" programming language and possibly easier to read
  1. Error handling code nicely separated (and not interleaved) from regular code

CON

  1. Error handling is far away from code that produce the error. Although this is a problem for all exception based error handling.
  1. Nasty Macros (although this is actually how exception works underneath in most other languages)
  1. Doesn't work if function within try block throws error. Although this isn't hard to fix if you are willing to introduce global state.
  1. setjmp / longjmp is expensive

#### Error string based

Based on the same ideas as [Return output via a reference argument](#return-output-via-a-reference-argument). But, we return the error code as string instead, so it is self describing. The string should preferably be const char * so that it hopefully doesn't require mmalloc.

```c
const char* foo(int *ret, int in1, int in2) {
  if(err) {
    return "OOM";
  }
}

const char* bar(int *v, int x, int y) {
  int val;
  const char* ret = NULL;
  if( (ret = foo(&val, x, y)) == NULL)
    goto cleanup;
  
  // use val here
  
cleanup:
  // resource free here
  return ret;
}

```

