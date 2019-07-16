### Java Basics
* Day 1 - JDK, JRE, JVM, Platform independence, compiler/interpreter

             Setting the path, classpath

             Some basic Java commands with JShell

             First helloworld program in Java

* Day 2 - Data types, built-in classes (java.lang, java.util, java.io etc)

            Operators - assignment, logical, conditional

             If-else if - else, for, while, do while, switch, 

* Day 3 - OOPs - Encapsulations, Inheritance, Polymorphism

* Day 4 - Collection API - Arrays, Hashmaps

* Day 5 - Access modifiers, Interfaces, Enums

* Day 6 - Exception handling

* Day 7 - File I/O

* Day 8 - Lambda

#### JDK, JRE, JVM, Compiler/Interpreter, Platform independence. 

A program is a set of instructions given to the computer to perform a process. The process can be as simple as adding two numbers to something very complex. Compilers and interpreters take the code which is written in human-writable-readable form and convert it to computer-readable form. In the case of programs that are written in languages which need compilation, there is a compiler which translates the code into bytecode. The target machine directly translates the bytecode into machine language. In this context, target machine is the machine in which the code is executed. In an interpreted language, the source code is directly translated by the target machine. Instead, the interpreter, reads and executes the code sequentially, in most cases. The disdvantage in this case is that it is time consuming; many programming errors are not apparent till the time of execution. 

Java has been around for more than 2 decades and JDK has constantly evolved all throughtout to now be the robust and stable OOP Language used in many huge applications. For this course we will use JDK 11. Please visit the <a href=" https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html">link</a> and download the compressed version that is meant for your operating system. For Mac it is gz file and for windows it is a zip file. 

1. Open the compressed file into a folder.
2. The bin folder inside the jdk folder contains all the executable files you need for Java. 
3. To set the java home on your system, open a terminal. At the command prompt, type `vscode ~/.bash_profile` open 
and paste this in the appropriate place. `export JAVA_HOME=/Users/lavanyas/Downloads/jdk-11.0.3.jdk/Contents/Home`. This command will ensure that the java home is set and you can compile and run the java programs from your terminal. 
4. Open a new terminal and type JShell. JShell is an extremely useful utility available from version Java 9 onwards, which allows you learn basic Java syntax, before you actually start writing programs. 
5. We will write some code to print our traditional 'Hello World'. 
<img src="jshell.png"/>
6. Type `System.out.println("Hello World!!")
7. `System.out` represents the standard output of the computer which is most cases is the console. This is the same as `console` in javascript. `System.in` represents the standard input which is the keyboard. We will look at an example using this later. 
8. Just like there are packages in javascript, there are packages in Java too which provide reusable components and code. The main packages which java has are
* java.lang - Provides classes that are fundamental to the design of the Java programming language.
* java.util - Contains the collections framework, some internationalization support classes (when you have to provide for multiple language support), a service loader, properties, random number generation, string parsing and scanning classes, base64 encoding and decoding, a bit array, and several miscellaneous utility classes. 
* java.io - Provides classes that handle I/O from standard I/O, Files, network, etc.,
* java.math - For all the math related functionalities
* java.net - For all network related functionalities
* java.sql - For all database and sql related functionalities
* java.time - For time and data related functionalilties 
* and many more such packages with specific functionalities and there are many more open source packages as well. All of these packages are available in a central repository called Maven. We will look at this at a later stage. For now, we will use the default packages that come with JDK. While working on the JShell, you don't have to do anything special to use the packages that come with JDK. 
9. In Java, all the statements have to end with a semicolon. ';' marks the end of the statement. JShell will execute single line commands like the one in step 6, without a semicolon. But that will not compile inside a Java program. However, in Java you can give multiple statements on the same line, as long as they are separated with a semi-colon. Try executing this on JShell.
`System.out.println("Hello World!");System.out.println("next line");`
10. 

We will use IntelliJ IDE for our learning and development purpose. Download the same from this <a href="https://www.jetbrains.com/idea/download/#section=mac">link</a>. We will use the community edition. 
1. 

