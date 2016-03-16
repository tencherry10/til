## On Error Handling

First off, a distinction need to be made between **errors** and **exception**:

- An error is a programing state / condition where it is impossible for the program itself to handle and 
  that a programmer must alter code in order to repair. Example of errors:

  1. Memory access error (SIGSEV) - an attempt by a program to access a memory page that it does not own. 
     Usually immediately terminated by the OS.
  1. Illegal instruction / opcode error - an attempt by a program to execute an illegal instruction. Very uncommon in the w/ the mature PC development enviornment, but is certainly possible with more exotic compilers.
  1. Instruction Priviledge error - an attempt by a program to execute an instruction that is not allowed in the current / cpu mode. 
  1. Not surprisingly, an unhandled exception is an error

- An exception denotes a relatively unpredictable and seldom condition that can (and should) be handled by the program itself. 
  Exceptions are generally defined by the programmer and/or the programming language.
  
  Here are some common exceptions:

  1. Memory exhaustion exception (OOM) - an attempt by the program to request more memory than the OS is willing to grant.
    Although this may be catastropic, it can be certainly be handled by the programmer. 
    A possible way is to unwind the current operation and free up as much memory as possible and wait until memory becomes available again.
  1. Divide by Zero exception - this may come as a surprise to many people but a processor will happily divide by zero. 
    It is usually the responsibility of the programmer to catch the divide by zero and 
    throw an exception and hope that the calling functions handles it.
  1. Overflow / Underflow exception - Just like divide-by-zero, there is no notion of overflow / underflow exception in the processor.     Sometimes this is even the anticpated/desirable behaviour. 
    Whether this is an exception and should be handled is up to the discretion of the programmer.
  1. Most input / output / file errors are actually exceptions - If you attempt to open a file that does not exist, it is an IO exception. The program can certainly recover from it. Confusingly enough, python calls this "exception" IOError...
  

So, a couple quick observations fall out from this:
  1. There are a lot more exceptions and exceptions are generally more meaningful than errors.
  1. Most people and languages confuse exceptions with errors (or more correctly programming mistakes). 

As a rule of thumb, a programming mistake could be categorized on two axis:
  1. Implicit/Explicit - whether the programmer is aware of the mistake
  1. Fatal/Non-fatal - whether the mistake was allowed to propagate or whether the program terminates itself

Let's give a couple examples
  1. Explicit+Fatal - 
    1. An assertion failed
    1. process exited with error code
  1. Explicit+Non-Fatal
    1. Logs error and give up and move on
    1. Drops packet (and hopes upstream retry)
    1. corrupt data
  1. Implicit+Fatal
    1. SEG FAULTS - (memory error but we have no idea why)
    1. Uncaught exception - (which exception caused it and where???)
  1. Implicit+Non-Fatal
    1. Programs survives but badly - everything is slow / grinds to a halt 
      (maybe thread-locked or waiting for a some back-pressured queue)
    1. Program cheerfully gives the wrong answer without awareness of error
    1. memory leaks / resource leaks

In the cases above, Hopefully it is obvious that Explicit + Fatal is most useful. We know where and why and we can proceed to triage the problem by looking at the core dump. 

Between Explicit+Non-Fatal and Implicit+Fatal, it is debatable which one is better or worse. Implicit+Fatal prevents the mistake from continuing (although it is painful to debug valgrind / gdb anyone?). Explicit+Non-Fatal gives you a bit more error info, but by the time you realized it, the program may have trashed your database.

Implicit+Non-Fatal is the worse of all, you may not even be aware of the error.

The solution? Handle **EVERY** exception. If it is handle-able, do it. If it is an obvious error, abort the program. Don't propagrate the error (unless you are library function).

