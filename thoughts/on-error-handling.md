## On Error Handling

First off, a distinction need to be made between **errors** and **exception**:

- An error is a programing state / condition where it is impossible for the program itself to handle and 
  that a programmer must alter code in order to repair. Example of errors:

  1. Memory access error (SIGSEV) - an attempt by a program to access a memory page that it does not own. 
     Usually immediately terminated by the OS.
  1. Not surprisingly, an unhandled exception is an error

- An exception denotes a relatively unpredictable and seldom condition that can (and should) be handled by the program itself. 
  Exceptions are generally defined by the programmer and/or the programming language.
  
  Here are some common exceptions:

  1. Memory exhaustion exception (OOM) - an attempt by the program to request more memory than the OS is willing to grant.
    Although this may be catastropic, it can be handled by the programmer. 
    A possible way is to unwind the current operation and free up as much memory as possible and wait until memory becomes available again.
  1. Divide by Zero exception - this may come as a surprise to many people but a processor will happily divide by zero. 
    It is usually the responsibility of the programmer to catch the divide by zero and 
    throw an exception and hope that the calling functions handles it.
  1. Overflow / Underflow exception - Just like divide-by-zero, there is no notion of overflow / underflow exception in the processor. 
    Sometimes this is even the anticpated/desirable behaviour. 
    Whether this is an exception and should be handled is up to the discretion of the programmer.
  
  

