
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

Effectively, what this does is only groups the variables together. You can have one structure inside the other. For instance, if you would now want to create an employee who will have the same attributes as person and in addition have  an employee number, you will have a structure inside a structure. 

```
#include <stdio.h>
#include <string.h>

struct person {
    char *name;
    int age;
    char *email;
};

struct employee {
    char *emp_code;
    struct person emp;
};

int main()
{
    struct employee e1;

    e1.emp.name = "Luca";
    e1.emp.age = 10;
    e1.emp.email = "lucacoote@gmail.com";
    e1.emp_code="E0001";
    
    printf("%s with employee code %s aged %d has email %s", e1.emp.name,e1.emp_code, e1.emp.age, e1.emp.email);    
   
    return 0;
}
```
You can see how it gets complicated as it does not allow for one structure to inherit from another. With more complex application, this gets not just too complex to code, but also too complex to bug fix and maintain.

To solve this problem, a new way to program was invented, called object-oriented programming (OOP). Object-oriented programming is a methodology that helps organize complex programs through the use of inheritance, encapsulation, and polymorphism. 

Let's try to work out the same with C++ which is an object oriented language. Copy and paste the code below in this link and execute it. https://www.tutorialspoint.com/compile_cpp_online.php. 

```
#include <iostream>  
using namespace std;  

class Person {  
   
   public:  
        string name;//data member(also called instance variable)      
        int age;//data member (also called instance variable)      
        string email;//data member (also called instance variable)      
    
};  

class Employee : public Person {
    public:
    string emp_code;
};

int main() {  
    Employee p1;    
    p1.name = "Luca";   
    p1.age = 201;   
    p1.email = "lucacoote@gmail.com";
    p1.emp_code = "E001";
    
    cout<<p1.name<<endl;  
    cout<<p1.age<<endl;  
    cout<<p1.email<<endl;  
    cout<<p1.emp_code<<endl;  
    return 0;  
}  
```
As you will find it very obvious in the code above, the class Employee inherits from class Person. So Employee has all features of a Person and other features of its own. When we created an object of class Employee, we could access all the attributes of the employee including that of the Person. We will discuss more in detail about Object oriented programming in the context of Java. 

C++ being a full-fledged OOP language was thought of as the final destination as it could handle all the complexity of code and was relatively easy to learn.  But the trouble with C and C++ (and most other languages) is that they are designed to be compiled for a specific target. Although it is possible to compile a C++ program for just about any type of CPU, to do sorequires a full C++ compiler targeted for that CPU. The problem is that compilers are expensive and time-consuming to create. An easier—and more cost-efficient—solution was needed. In an attempt to find such a solution, Gosling and others began work on a portable, platform-independent language that could be used to produce code that would run on a variety of CPUs under differing environments. This effort ultimately led to the
creation of Java.

Reference: The Complete Reference 9th Edition.
