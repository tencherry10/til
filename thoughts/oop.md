### Thoughts on OOP

1. [What is OOP?](#what-is-oop)
1. [OOP and Encapsulation / Inheritance / Polymorphism](#oop-is-orthogonal-to-encapsulation--inheritance--polymorphism)
1. [Duck Typing and OOP](#duck-typing-and-oop)

---

#### What is OOP?

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

#### OOP is orthogonal to Encapsulation / Inheritance / Polymorphism

Perhaps the most important point to realize is that OOP does not provide Encapsulation / Inheritance / Polymorphism. In reality, the relationship is opposite, you must have Encapsulation / Inheritance / Polymorphism before you can have OOP. So, you can have Encapsulation, Inheritance, and even Polymorphism in pieces (or all) without having OOP.

Case in point, let's look at C examples of how we can implement some or portions of OOP. C is chosen here b/c it is the prime example of a programming language that doesn't implement OOP intrinsically.

1. Look at the implementation of FILE inside the libc library. It implements **Polymorphism** / **Encapsulation** functionality (ability to read/write from/to file streams) without Inheritance in C. It does it using a virtual dispatch jump table.
1. Using opaque structs and a collection of public classes in C, one can easily **Encapsulate** the details from the client. For an interesting example of this, take a look at lua's code at lua_State.
1. You can also just get **Inheritance** using just C struct sharing. You can also use ```-fms-extensions``` and annonymous structs to make this even more seamless.
1. Take a look at gnome's [GObject](https://developer.gnome.org/gobject/stable/). It impements the whole OOP lifecycle with all of **Polymorphism** / **Inheritance** / **Encapsulation**.
1. IF GObject is too heavy for you, you can also roll **Polymorphism** / **Encapsulation** class system on your own using a combination of virtual dispatch jump table with opaque structs. For an example, see this [sample code](https://github.com/tencherry10/learn/tree/master/c_vtable). You can easily extend this with C structural sharing in order to get **Inheritance**.
 
#### Duck Typing and OOP

As an aside, OOP can be "emulated" and portions of its feature can be "compromised". 

For e.g., in python, it is possible to just polymorphically substitute an object with another object that is unrelated in terms of inheritance but have a similar method signature. 

This notion of duck-typing means that an object is substitute-able with another object provided its API is the same (if it quacks like a "Duck"). This is great for dynamic languages and reduces the burden / ceremony of OOP, but may not be possible for static languages which demands compile time binding. 

BTW, this duck-typing does NOT require that all API/method is implemented. Only the API/method used is necessary as there are no enforcement from the compiler/interpreter during duck-typing. (an exception is simply thrown when an unimplemented function are called).

There is also a question of performance b/c this means the compiler / interpreter can not optimize across polymorphic late-binding boundary. Although, technically a JIT could work around this issue.





