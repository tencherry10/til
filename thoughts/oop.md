### OOP

The distinctive features of Object-Oriented Programming are:

1. Encapsulation - Hiding state / details behind the Object's API (or methods). 
  
  The main goal of Encapsulation is separation of concerns, 
  changing the private implementation details of an object should not break its clients' code.

  Also, as a secondary "feature", Encapsulation draws a clear boundary between what is implementation and what is interface.

1. Inheritance - Code reuse mechanism via cloning of state and methods. 
  
  The actual details vary from language to language. For e.g. 
  - In Java method inheritance is automatic unless you opt-out with final
  - In C++ inheritance is not enabled unless you opt-in with virtual
  - In javascript the inheritance is based on an existing prototype (rather than a template)
  - In lua the inheritance is based on a "meta" table which you can manipulate quite like a regular table
  
  The point is that inheritance as code reuse means different things in different language

1. Polymorphism - Provides a mechanism for selecting a proper procedural method call via Dynamic Dispatch specifically on the type of the object.

### Thoughts

Immediately, the first things to recognize is OOP does not provide Encapsulation / Inheritance / Polymorphism. In reality, the relationship is opposite, you must have Encapsulation / Inheritance / Polymorphism before you can have OOP. So, you can have Encapsulation, Inheritance, and even Polymorphism in pieces (or all) without having OOP.

Case in point, let's look at C examples of how we can implement some or portions of OOP. C is chosen here b/c it is the prime example of a programming language that doesn't implement OOP intrinsically.

1. Look at the implementation of FILE inside the libc library. It implements **Polymorphism** / **Encapsulation** functionality (ability to read/write from/to file streams) without Inheritance in C. It does it using a virtual dispatch jump table.
1. Using opaque structs and a collection of public classes in C, one can easily **Encapsulate** the details from the client. For an interesting example of this, take a look at lua's code at lua_State.
1. Take a look at gnome's [GObject](https://developer.gnome.org/gobject/stable/). It impements the whole OOP lifecycle with all of **Polymorphism** / **Inheritance** / **Encapsulation**.





