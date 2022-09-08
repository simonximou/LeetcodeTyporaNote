# The Art of Computer Science

## Programming Languages 

### Java

#### Some Useful method/data structure/code

####  

#### Java Classes 



#### JVM

A **Java virtual machine** (**JVM**) is a [virtual machine](https://en.wikipedia.org/wiki/Virtual_machine) that enables a computer to run [Java](https://en.wikipedia.org/wiki/Java_(software_platform)) programs as well as programs written in [other languages](https://en.wikipedia.org/wiki/List_of_JVM_languages) that are also compiled to [Java bytecode](https://en.wikipedia.org/wiki/Java_bytecode).

The **JVM** performs following operation:

- Loads code
- Verifies code
- Executes code
- Provides runtime environment

**JVM** provides definitions for the:

- Memory area
- Class file format
- Register set
- Garbage-collected heap
- Fatal error reporting etc.

JVM Architecture

Let's understand the internal architecture of JVM. It contains classloader, memory area, execution engine etc.

![JVM Architecture](https://static.javatpoint.com/images/jvm-architecture.png)

1) **Classloader**

Classloader is a subsystem of JVM which is used to load class files. Whenever we run the java program, it is loaded first by the classloader. There are three built-in classloaders in Java.

1. **Bootstrap ClassLoader**: This is the first classloader which is the super class of Extension classloader. It loads the *rt.jar* file which contains all class files of Java Standard Edition like java.lang package classes, java.net package classes, java.util package classes, java.io package classes, java.sql package classes etc.
2. **Extension ClassLoader**: This is the child classloader of Bootstrap and parent classloader of System classloader. It loades the jar files located inside *$JAVA_HOME/jre/lib/ext* directory.
3. **System/Application ClassLoader**: This is the child classloader of Extension classloader. It loads the classfiles from classpath. By default, classpath is set to current directory. You can change the classpath using "-cp" or "-classpath" switch. It is also known as Application classloader.

These are the internal classloaders provided by Java. If you want to create your own classloader, you need to extend the ClassLoader class.

2) **Class(Method) Area**

Class(Method) Area stores per-class structures such as the runtime constant pool, field and method data, the code for methods.

3) **Heap**

It is the runtime data area in which objects are allocated.

4) **Stack**

Java Stack stores frames. It holds local variables and partial results, and plays a part in method invocation and return.

Each thread has a private JVM stack, created at the same time as thread.

A new frame is created each time a method is invoked. A frame is destroyed when its method invocation completes.

5) **Program Counter Register**

PC (program counter) register contains the address of the Java virtual machine instruction currently being executed.

6) **Native Method Stack**

It contains all the native methods used in the application.

7) **Execution Engine**

It contains:

1. A virtual processor
2. Interpreter: Read bytecode stream then execute the instructions.
3. Just-In-Time(JIT) compiler: It is used to improve the performance. JIT compiles parts of the byte code that have similar functionality at the same time, and hence reduces the amount of time needed for compilation. Here, the term "compiler" refers to a translator from the instruction set of a Java virtual machine (JVM) to the instruction set of a specific CPU.8) Java Native Interface

Java Native Interface (JNI) is a framework which provides an interface to communicate with another application written in another language like C, C++, Assembly etc. Java uses JNI framework to send output to the Console or interact with OS libraries.

#### Compilation 

In Java, programs are not compiled into executable files; they are compiled into [bytecode](https://en.wikipedia.org/wiki/Bytecode) (as discussed [earlier](https://en.wikibooks.org/wiki/Java_Programming/The_Java_Platform)), which the JVM (Java Virtual Machine) then executes at runtime. Java source code is compiled into bytecode when we use the `javac` compiler. The bytecode gets saved on the disk with the file extension `.class`. When the program is to be run, the bytecode is converted, using the [just-in-time](https://en.wikipedia.org/wiki/Just-in-time_compilation) (JIT) compiler. The result is machine code which is then fed to the memory and is executed.

Java code needs to be compiled twice in order to be executed:

1. Java programs need to be compiled to bytecode.
2. When the bytecode is run, it needs to be converted to machine code.

The Java classes/bytecode are compiled to machine code and loaded into memory by the JVM when needed the first time. This is different from other languages like C/C++ where programs are to be compiled to machine code and linked to create an executable file before it can be executed

Can usually catch mistaally kes or syntax error before running. 

#### Advantage 

Java manage the memory for you, better than C++. Automatically return the memory to the computer, where C++ have to do that manually. But remember it will be slower. Speed wise, C++ > Java > Python

Compilation process will provide syntax error check while compiling 

Not sure if it is an advantage but as a statically typed programming, you have to identify the data type when assigning the variable. int a = 1. 

#### Type Casting 

**Java Type Casting**

Type casting is when you assign a value of one primitive data type to another type.

In Java, there are two types of casting:

- **Widening Casting** (automatically) - converting a smaller type to a larger type size
  `byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double`

  

- **Narrowing Casting** (manually) - converting a larger type to a smaller size type
  `double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte`

------



### Python



### JavaScript



### CSS



### C



### C++



## Computer System

## Computer Network

## Database

## System Design

## OOP

### Advantages of OOP

OOP stands for **Object-Oriented Programming**.

Procedural programming is about writing procedures or methods that perform operations on the data, while object-oriented programming is about creating objects that contain both data and methods.

Object-oriented programming has several advantages over procedural programming:

- OOP is faster and easier to execute
- OOP provides a clear structure for the programs
- OOP helps to keep the Java code DRY "Don't Repeat Yourself", and makes the code easier to maintain, modify and debug
- OOP makes it possible to create full reusable applications with less code and shorter development time

### Encapsulation



### Abstraction

### Inheritance

![image-20220202184547127](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20220202184547127.png)

The children class Inherit the parent class.

- save time and extra coding since we can write one class and inherit it anytime we need 
- 



### Polymorphism