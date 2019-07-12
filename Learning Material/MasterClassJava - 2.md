### Before the master class you must have

* Java 1.8 or above installed in your computer. On your terminal, type “java –version” to determine that you have the right version
* Install SpringToolSuite from spring.io https://spring.io/tools3/sts/all which is meant for your operating system
(We will spend a while initially to make sure everyone has the installation in place before proceeding to learn)


### Class in Java 

In python, you may recollect everything is a module. Everything in Java is a class. Literally everything. When you write the simplest  application to print *Hello World*, even that is a class. It is called a Runnable Class. 

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
 Java langauge grammar thrives on { } and ;. Every block of code in Java has to be within {} and every statement which is to be executed should end with ;. You may recollect the tab spacing in Python. { ... } serves the same purpose here. 
 
 Try a few things:
 1. Try removing the word public in the class. 
 2. Try switching public and static in the main method. 
 3. Try removing the word public in the main method.
 4. Try removing the word static in the main method.

### Things you should know about Java
1. To run a class it has to be a public class
2. You run a runnable class with its classname `java <name of the class>`
3. The class should have a public static void main method which takes a String [] argument.
4. The String [] argument is nothing but the command line arguments you give the class when you run it. You can refer to the string array with any variable name. Commonly used ones as *s* and *args*.
5. A class has to be written in a file with the extension Java.
6. A class is first compiled and then run. Compilation is the process of converting the source Java file into bytecodes, which the JVM understands. A class can be compiled on one system and run on another system - Platform independence 
7. When you compile a .java file, it produces a .class file with the same name if the compilation is successful. The .class file contains bytecodes (non-human readable form) which can be interpreted by an Operating System which has Java Runtime Environment set up. 
8. Most computers in the modern days have Java Runtime Environment.


### JVM 
JVM stands for Java Virtual Machine. It is a Virtual Machine which understands bytecodes and can load a class object, allocate and manage memory for all the objects which are in-turn required. The analogy is like a Windows Media player application which knows to read mp3 files and produce music from it. JVM is not platform independent. There is JRE for each kind of operating system. The `java` application in the JRE starts the JVM.

In the example we saw above, can you identify the classes that would be loaded in the JVM?

### OOPs they did it again:

The foundation of Object Oriented Programming is Inheritance, Data Encapsulation, Over-riding, Over-loading and Polymorphism. Before we head on to understand what each of this are, let's scaffold Objects. Clone this repository and import it into a java project folder in STS for further learning. https://github.com/lauvshree/javaexamples.git


Object Oriented Programming as the name says is based on Objects. What are objects? Objects are instances of a class. 

Classes are more like reusable templates. Look at the images below.

#### Class

<img src="ClubMemberClass.png" width="200px">

#### Object 

<img src="ClubMemberObject.png" width="200px">

### Members of a class
A class can have attributes, methods and special methods called constructors.

Attributes are distinct features of the class. The attributes can have different kind of access. They can be public, protected, private or default (default is when you specify nothing; don't actually write the word default). Attributes can be static or non-static (again, non-static is when you give nothing; don't actually write the word non-static). Static like the word implies, makes the attribute static. It will have the same value for all the instances of the class. When a member is non-static, it will have a different value for each object.

Let's create this class in the STS IDE.

```
public class APEmployee {
	priavte String name = null;
	private String emp_code = null;
	private static String companyName = "Australia Post";
}
```


#### Template for attribute definition:
```
<access modifier> <non-access modifier> <data type> <variable name> = <initial value>;
```


#### Template for method definition:
```
<access modifier>   <non-access modifier>   <return data type>   <method name> 

{
	......
}	
```


<table>
	<tr>
		<td>
			access modifier
		</td>	
		<td>
			public, private, protected, default
		</td>
	</tr><tr>
		<td>
			non-access modifier
		</td>	
		<td>
			static, non-static
		</td>
	</tr><tr>
		<td>
			data type
		</td>	
		<td>
			primitive data type, Java classes, user-defined classes 
		</td>
	</tr><tr>
		<td>
			name
		</td>
		<td>
			Can be anything. Convention start with small letter. If it is compund words, start the consequtive words with uppercase eg., getUserName
		</td>
	</tr>
</table>
	

Methods are callable functions you can call on the objects of the class. They can be doing simple things like printing a message or a very complex thing. Most modern day IDEs will have generator for standard methods which are expected to be in a class. 

Let's generate some methods in the IDE for the APEmployee class we created. 

Before we can access attributes or methods of an object, we need to create an object. To create object or rather construct objects we use constructors.

#### Constructors
These are special methods, which have the same name as the class and have no return types. They have implicit return types and they always return and object of the class. We follow the syntax below to create Objects.

`APEmployee apEmployee1 = new APEmployee();`

Let's create a runnable class, create an Object of APEmployee and invoke the generated methods.

```
public class EmployeeGenerator {

	public static void main(String[] args) {
		
		APEmployee.setCompanyName("Australia Post");

		APEmployee apEmployee1 = new APEmployee();
		apEmployee1.setEmpCode("E001");
		apEmployee1.setName("Phil Jackson");
		
		System.out.println(apEmployee1);
		
		APEmployee apEmployee2 = new APEmployee();
		apEmployee2.setEmpCode("E002");
		apEmployee2.setName("Linah Wafai");
		
		System.out.println(apEmployee2);
	}

}
```

These constructors, which take no arguments, do not have to be explicitly defined. In the above example, we used the constructor though we never defined it when we created the class. This was possible because Java implicitly does it for us. But you can define constructors for the class. You can even have more than one constructor.

```
public class APEmployee {
	priavte String name = null;
	private String emp_code = null;
	private static String companyName = "Australia Post";
	private static int empCount = 0;
	private static String empCodePrefix = "E00";

	public APEmployee() {
		System.out.println("Object is created. No initial values set yet");
	}
	
	public APEmployee(String name) {
		//this refers to the current object
		this.name = name;
		this.emp_code = empCodePrefix+(++empCount);
	}		
}
```
*this is similar to the self in Python. It is how the object can refer to itself*

#### Point to ponder

Why do you have the attributes as private and then provide public methods to access them? Doesn't it make it simpler to make the attributes public? 


Think of the class APEmployee having public attribute name instead of private attribute name. We can set 
`apEmployee1.name = <anything that qualifies as a string>`

But we want name to only be string of alphabets. Or for instance I want age only between 18 to 60. All these validations can be handled in the setter. That is why the attribute is kept private and is allowed access only through setters and getters. This is not mandatory. It is a tried and tested coding practice.


#### Loading a class and creating an object
When we run a class, we load the class. Loading a class is when the bytecodes are read and the class is ready for use. We only create an object when we call the `new <constructor>`. 

Classes can be grouped together in packages. Java provides many packages to facilitate coding. 
* java.lang
* java.util
* java.io
* java.math
and so on. 

All of the java.lang package classes are also loaded and kept ready for use in any java code you write. That is why we didn't have to do anything special to let the system know we are using the java.lang package. Any other package you need, have to be explicitly imported. 

User defined classes can also be organized into packages. To create a package, we start the code with package definition. 
`package com.auspost.firstjavaclass;`. This should be the first statement before you import other packages/classes you want to use. 


To read the input line by line from the user we use `Scanner` object from the java.util package. This object takes an input stream as an argument to the constructor. We will pass the System.in which is the keyboard input stream. Since java.util package is not loaded by default, we need to import it with `import java.util.Scanner;`

Let's make a new EmployeeGenerator which will create the Object only when the user requests for it.


```
//It will load the class Scanner
import java.util.Scanner;

//All the classes in java.lang package will be loaded by default

//The main runnable class which will be loaded
//APEmplyee Class will be loaded
public class EmployeeGeneratorAtWill {
	
    public static void main(String s[]) throws Exception {
    	//A String object is created. Do you see there is no new here? This is only allowed for Strings, Integer and other primitive data type wrappers
        String reply = "y";
        //A primitive int is created
        int i = 1;
        //Creating a scanner object which will read from the System's input
        Scanner scanner = new Scanner(System.in);
        //A string object is created and printed out on the System output
        System.out.println("Do you want to create an Employee ");
        //A line is read from the System input until enter is pressed and stored in reply
        reply = scanner.nextLine();            
        
        while(reply.equalsIgnoreCase("y")) {
            //A new APEmployee object is created
        	APEmployee ap = new APEmployee();
            //A string object is created and printed out on the System output
            System.out.println("Enter employee name ");
            //A line is read from the System input until enter is pressed and stored in name
            String name = scanner.nextLine();
            ap.setName(name);
            ap.setEmpCode("E00"+i++);
            //The toStringMethod is invoked on the ap object
            System.out.println(ap);
            //A string object is created and printed out on the System output
            System.out.println("Do you want to create another an Employee ");
            //A line is read from the System input until enter is pressed and stored in reply
            reply = scanner.nextLine();            
        }
        //Close the scanner
        scanner.close();
    }
}
```

The idea of making it all classes was to make it reusable to the best possible extent. There are more than one way in which class can be used. 
* We can create the object - That's what we did with the `new <Constructor>` 
* We can inherit from the class

#### Inheritance
```
public class APContractEmployee extends APEmployee {
	
	priavte String name = null;
	private String emp_code = null;
	private static String companyName = "Australia Post";
	private static int empCount = 0;
	private static String empCodePrefix = "CE00";
}
```

When a class extends another class, it is called a **subclass**. The class which it extends, is called the **superclass**. 

* When a variable or method has default access, these members are available all over the package to which the class belongs.  The other possible access are:

* When a variable or method has private access, it is private to the class. Cannot be accessed anywhere outside the class. 

* When a variable or method has public access, it is public and is available through an object of the class anytime. 

* When a variable or method has protected access, its access is restricted to the package the class is a part of and the subclasses. 

All classes by default extend from Object class in java.lang package, implicitly.


#### Data Encapsulation
This is the ability to define the access of the variable and methods in a class. 

#### Over-riding
When a subclass overrides a super class method or variable within itself, it is called over-riding. 

#### Over-loading
When there are multiple method with same name and return type, but different argument types, it is called overloading.

#### Polymorphism
When the same method invoked on a reference object behaves in different ways depending on the object it is invoked upon, it is called polymorphism. Poly - many, morph-different form. 



