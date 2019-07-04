Everything in Java is a class. Literally everything. When you write the simplest traditional application to print *Hello World*, even that is a class. It is called a Runnable Class. 

https://www.tutorialspoint.com/compile_java_online.php

Let's write our first Runnable class in the above link and try it out. 


The idea of making it all classes was to make it reusable to the best possible extent while harnessing the  

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
