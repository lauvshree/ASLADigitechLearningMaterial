#### Before developing a spring boot application you must have
* Java 1.8 or above installed in your computer. 
* Installed SpringToolSuite
* Be familiar with class, object and OOPs concept.

#### Objective of this session
At the end of this session you must have created a full stack application using Java SpringBoot. 

#### Prelude to Spring Maven projects
Spring is a framework which can be used to create Java full stack development. In Java, there are some classes available in packages as a part of the Java Standard Edition and many other external jars(Java ARchives) which have constantly evolved over 20 years. All these jars are in a common repository called maven (mvnrepository.com). Before the days of Spring and Maven, you had to download each jar and ensure they are in the classpath for them to be used in you classes. Spring Maven brought about a revolution. The Maven projects have a pom.xml (Project Object Model) where you just include the list of dependencies and all of that is download from maven seamlessly. To learn more about pom, go to https://maven.apache.org/guides/introduction/introduction-to-the-pom.html.

SpringBoot is custom made with the modern-day developer in mind. All that the developer has to do to create a full stack web application is include one dependency which will in turn load all the dependent files, leaving the developer to better utilise her/his time. But the developer has to stick to the convention of including the dependency as expected. Else it miight not work as expected. 


#### Step by Step full stack app
1. Launch STS
2. Create a new Maven Project. 
  * Check the option *"Create a simple project"*
  * Click on the *Next* button
  * It asks for a GroupId and Artifact id. Enter some appropriate names. Suggestion: Group Id: com.auspost ArtifactId: example
  * Go to your pom.xml and include the following dependency just above the <dependencies> tag. 
  
  ```
	<parent>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-parent</artifactId>
	    <version>2.1.6.RELEASE</version>
	</parent>

  ```

*This tells maven that this project is a child of Spring Boot Starter Parent. All the default configuration is automatically done for you*

3. As we are creating a web application, we will now include a dependency for the web starter kit. Again this downloads all the jars you need to create REST services. In the pom.xml include the following inside the `dependencies` tag.
  
  ```
  	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-web</artifactId>
	</dependency>

  ```
  *Once you do the above steps and save, you will see a Maven Dependencies is generated in the project folder with all the jars.*
4. If the JRE that is being pointed to is not 1.8, we need to change it to use 1.8. Right click on you project folder, click on `Build Path` choose `Configure Build Path`. Make sure `Java Build Path` is highlighted in the left pane. In the `Libraries` tab. Click on JRE 1.5 and click on `Remove`. Then, click on `Add Library`. Choose `JRE System Library` and click `Next`. Select `Workspace default JRE` if not already selected and then click on `Finish`. Go to the `Order and Export` tab and check `Maven Dependencies` and `JRE System Library`. Click on `Apply and Close`.
5. Right click on the project folder and create a new class, with a `main` method. As we saw earlier, this is just a simple java Runnable class. 
6. We use something called annotations which tell the Java compiler what kind of application this is. We are trying to create a SpringBootApplication. We will add this annotation `@SprintBootApplication` to the class. This will mark you with an error and prompt you to import and use appropriate class to understand the annotation. The IDE will magically do this for you.
7. Now all that we have to do is start a server instance, which will start this Runnable class as a SpringBoot application. 
  ```
  package com.lavjava.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class App 
{
    public static void main( String[] args )
    {
    //Pass the name of the class which is annotated as a SpringBootApplication and args
    	SpringApplication.run(App.class, args);
    }
}

```
8. Now let's create an end point which we want to serve on our server. Right click on the parent folder of your java application, and create a new `package` and name it `controller`. It can be anything, but we are naming it controller for clarity.
9. Within the new created package, right click and create a new class called `MyServerController`(Call it whatever you want. It is just a name :)). This class is going to be our RestController. So we will annotate the class with `@RestController` 

10. We will now ammend the class, to provide our first resource mapping. 

```
package com.lavjava.example.controller;

import java.net.URISyntaxException;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyServerController {

	@RequestMapping("/hello")
	public String hello( ) throws URISyntaxException {
		return "Hello Gorgeous!";
	}
}

```
11. Now if there are no red-flags and every thing compiles fine, right click on the project root folder and choose `Run As` and click on `Spring Boot App`. On your browser access 'localhost:8080/hello' and see what you get. 

If you saw "Hello Gorgeous!", congratulations!! You just created your first Java REST end point. Woo hoo!

We returned a truthy String to all the gorgeous people. But we want to be able to do more than that. We will create a web application which allow us to add person details, get details of a person with his email id and get list of of persons in the DB. 

Continuing from where we left,

12. Follow the same steps as in step 8 and create a new package called models. 
13. In models, create a class called Person with three String attributes - name, email and phone. Generate the getters and setters and toString method.
14. Go back to the MyServerController and add another end point which which return a person.
```
	@RequestMapping("/person")
	public Person getPerson( ) throws URISyntaxException {
		Person p1 = new Person();
		p1.setName("Jason Burns");
		p1.setEmail("jason.burns@gmail.com");
		p1.setPhone("0499998888");
		return p1;
	}
```
15. Now restart server and access the new end point we have created on your browser or postman. 'localhost:8080/person'. Do you see what you expected to see? The output on browser should be `{"name":"Jason Burns","email":"jason.burns@gmail.com","phone":"0499998888"}`

16. We will add and endpoint now to provide for adding a Person. We will also include a HashMap object to store the values of Persons created, which is a key-value table, in our case the key being the emailId and value being the Person itself. Add the following lines of code to the MyServerController.
```
HashMap<String,Person> hmapPersons = new HashMap<String, Person>();
	
@RequestMapping(value = "/person", method = RequestMethod.POST)
public String getPersonInfo(@RequestBody Person person) {
	hmapPersons.put(person.getEmail(), person);
	return "Person added";
}

```
17. We will also change the `get` end point to get the person from the HashMap based on the email id. 
```
@RequestMapping("/person/{email}")
public Person getPersonInfo(@PathVariable String email) {
	return hmapPersons.get(email);
}

```

18. Before we restart let's also make another endpoint to get all the Persons in the HashMap.
```
@RequestMapping("/persons")
public Person[] getPerson( ) throws URISyntaxException {
	Person[] personCollection = new Person[hmapPersons.size()];
	//Copy all the values in the hashMap to an array and return it
	return hmapPersons.values().toArray(personCollection);
}

```
19. Save all the code and restart the server (If you are wondering why we are not compiling, STS does it automatically for you). Test all the end points we just created with postman. Sample data for input:
`{"name":"Jason Burns","email":"jason.burns@gmail.com","phone":"0499998888"}`




  
  
  