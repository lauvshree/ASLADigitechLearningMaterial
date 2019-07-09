### Before the master class you must have

* Java 1.8 or above installed in your computer. On your terminal, type “java –version” to determine that you have the right version
* Install SpringToolSuite from spring.io https://spring.io/tools3/sts/all which is meant for your operating system
(We will spend a while initially to make sure everyone has the installation in place before proceeding to learn)


### Class in Java 

In python, you may recollect everything is a module. Everything in Java is a class. Literally everything. When you write the simplest traditional application to print *Hello World*, even that is a class. It is called a Runnable Class. 

#### How to create a class

Let's write our first Runnable class in the following link and try it out.

https://www.tutorialspoint.com/compile_java_online.php


 ```
 public class MyFirstRunnableClass {
    public static void main(String s[]) {
        System.out.println("Hello World");
    }
}
 ```
 
 Try a few things:
 1. Try removing the word public in the class. 
 2. Try switching public and static in the main method. 
 3. Try removing the word public in the main method.
 4. Try removing the word static in the main method.

### Things you should know about Java
1. To run a class it has to be a public class
2. You run a runnable class with its classname `java <name of the class>`
3. The class should have a public static void main method which takes a String [] argument.
4. The String [] argument is nothing but the command line arguments you give the class when you run it. You can refer to the string array with any variable name. Commonly used ones as s and args.
5. A class has to be written in a file with the extension Java.
6. A class is first compiled and then run. A class can be compiled on one system and run on another system - Platform independence 
7. When you compile a .java file, it produces a .class file with the same name if the compilation is successful. The .class file contains bytecodes (non-human readable form) which can be interpreted by an Operating System which has Java Runtime Environment set up. 
8. Most computers in the modern days have Java Runtime Environment.


### JVM 
JVM stands for Java Virtual Machine. It is a Virtual Machine which understands bytecodes and can load a class object, allocate and manage memory for all the objects which are in-turn required. The analogy is like a Windows Media player application which knows to read mp3 files and produce music from it. JVM is not platform independent. There is JRE for each kind of operating system. They `java` application in the JRE starts the JVM.

In the example we saw above, can you identify the classes that would be loaded in the JVM?


### Members of a class
A class can have attibutes, methods and special methods called constructors.

attributes - 


The idea of making it all classes was to make it reusable to the best possible extent.

### OOPs they did it again:

Object Oriented Programming as the name says is based on Objects. What are objects? Objects are instances of a class. 

Classes are more like reusable templates. They have certain attributes. Look at the images below.

![Class](ClubMemberClass.png)



![Object](ClubMemberObject.png)

The class provides methods called setters and getters which help set values of these attributes and get values of these attributes. The class will also provide other methods that can be invoked on the object. 

```
public class Customer {
	
	String name;
	String email;

}
```
The attributes and methods of a class can have different access. They can be public, private, protected or when nothing is mentioned, have default access. Most attributes of a class are kept as private members. 
