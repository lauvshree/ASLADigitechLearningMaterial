
Java is an Objected Oriented language and has been around for more than 20 years now. It was built with an intent of making an OS indendent language - Write once, run anywhere. This may sound very alien to the stage at which the technological evolution has brought us today but the fact is the predecessors of Java had to be compiled and run in each OS with System specific compilers and interpreters. 

Any new Computer language innovation and development occurs for two fundamental
reasons:
•	 To adapt to changing environments and uses
•	 To implement refinements and improvements in the art of programming

There are many languages and new ones every now and then which testify the above statements. The predecessor of Java is C++. C language is the predecessor of C++. C came into being to satisfy the need for an was an efficient programming language which could be used for complex programming and was at the same time easy to learn. C had support for structures which are similar to the class attributes in the Object Oriented langauages. But the structures had to be used as is and it was more of a virtual grouping than reusable components. 
Structure is a collection of variables under a single name.

For example: You want to store information about a person: his/her name, age and email. If you now want to store information about 3 persons, we will end up doing:

```
name1 = ...
ag11 = ...
email1 = ...

name2 = ...
age2 = ...
email2 = ...

name3 = ...
age3 = ...
email3 = ...

```
You can imagine how complex this will get if you have to store information about 100s or 1000s of users. Putting them in struct, helps solve this issue to some extent. Try the following code out https://www.tutorialspoint.com/compile_c_online.php

```
#include <stdio.h>
#include <string.h>

struct person {
    char *name;
    int age;
    char email[50];
};

int main()
{
    struct person p1,*p2;

    p1.name = "Luca";
    p1.age = 10;
    strcpy(p1.email,"lucacoote@gmail.com");
    
    printf("%s aged %d has email %s",p1.name,p1.age,p1.email);    
   
    return 0;
}
```

Effectively, what this does is only groups the variables together. You can have one structure inside the other. But as the code gets complex the structures will get more complex.

To solve this problem, a new way to program was invented, called object-oriented programming (OOP). Object-oriented programming is a methodology that helps organize complex programs through the use of inheritance, encapsulation, and polymorphism. 


