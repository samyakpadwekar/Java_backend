# Spring-Core-Interview-Question

### 1.what is spring framework?
- Spring Framework is a Java platform that provides comprehensive infrastructure support for developing Java applications. Spring handles the infrastructure so you can focus on your application.
- Spring enables you to build applications from “plain old Java objects” (POJOs) and to apply enterprise services non-invasively to POJOs. This capability applies to the Java SE programming model and to full and partial Java EE.
- Examples of how you, as an application developer, can use the Spring platform advantage:
a. Make a Java method execute in a database transaction without having to deal with transaction APIs.
b. Make a local Java method a remote procedure without having to deal with remote APIs.
c. Make a local Java method a management operation without having to deal with JMX APIs.
d. Make a local Java method a message handler without having to deal with JMS APIs.

### 2.what are the features of spring?
1. *IoC container* - Refers to the core container that uses the DI or IoC pattern to implicitly provide an object reference in a class during runtime.
2. *Data access framework* - Allows the developers to use persistence APIs, such as JDBC and Hibernate, for storing persistence data in database.
3. *Spring MVC framework* - Allows you to build Web applications based on MVC architecture.
4. *Transaction management* - Helps in handling transaction management of an application without affecting its code.
5. *Spring Web Service* - Generates Web service endpoints and definitions based on Java classes, but it is difficult to manage them in an application..
6. *JDBC abstraction layer* - Helps the users in handling errors in an easy and efficient manner.
7. *Spring TestContext framework* - Provides facilities of unit and integration testing for the Spring applications.

### 3.what are the modules of spring?
<img src="https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/images/spring-overview.png" width="600" height="400">

1. **Core Container**
- The Core Container consists of the Core, Beans, Context, and Expression Language modules.
- The *Core* and *Beans* modules provide the fundamental parts of the framework, including the IoC and Dependency Injection features.
- The *Context* module builds on the solid base provided by the Core and Beans modules: it is a means to access objects in a framework-style manner that is similar to a JNDI registry. The *Context* module inherits its features from the Beans module and adds support for internationalization, event-propagation, resource-loading, and the transparent creation of contexts by, for example, a servlet container, has supports Java EE features such as EJB, JMX ,and basic remoting. The ApplicationContext interface is the focal point of the Context module.
- The *Expression Language* module provides a powerful expression language for querying and manipulating an object graph at runtime.

2. **Data Access/Integration**
- The Data Access/Integration layer consists of the JDBC, ORM, OXM, JMS and Transaction modules.
- The *JDBC* module provides a JDBC-abstraction layer that removes the need to do tedious JDBC coding and parsing of database-vendor specific error codes.
- The *ORM* module provides integration layers for popular object-relational mapping APIs, including JPA, JDO, Hibernate, and iBatis.
- The *Java Messaging Service (JMS)* module contains features for producing and consuming messages.
- The *Transaction module* supports programmatic and declarative transaction management for classes that implement special interfaces and for all your POJOs (plain old Java objects).

3. **Web**
- The Web layer consists of the Web, Web-Servlet, Web-Struts, and Web-Portlet modules.
- Spring's Web module provides basic web-oriented integration features such as multipart file-upload functionality and the initialization of the IoC container using servlet listeners and a web-oriented application context. It also contains the web-related parts of Spring's remoting support.
- The *Web-Servlet* module contains Spring's model-view-controller (MVC) implementation for web applications.
- The *Web-Portlet* module provides the MVC implementation to be used in a portlet environment and mirrors the functionality of Web-Servlet module.

4. **AOP and Instrumentation**
- Spring's *AOP* module provides an AOP Alliance-compliant aspect-oriented programming implementation allowing you to define, for example, method-interceptors and pointcuts to cleanly decouple code that implements functionality that should be separated.
- The separate *Aspects* module provides integration with AspectJ.
- The *Instrumentation* module provides class instrumentation support and classloader implementations to be used in certain application servers.

5. **Test**
- The Test module supports the testing of Spring components with JUnit or TestNG. It provides consistent loading of Spring ApplicationContexts and caching of those contexts. It also provides mock objects that you can use to test your code in isolation.

### 4.What is Loose Coupling?
- Loose coupling is a concept in software engineering and system design that describes the degree to which components or modules within a system are independent of each other and interact with minimal dependencies.
- It is a fundamental principle in designing software systems and is often associated with the goal of making systems more maintainable, flexible, and scalable.
- Here are some key characteristics and advantages of loose coupling:
1. *Independence*
2. *Minimal Dependencies*
3. *Flexibility*
4. *Reusability*
5. *Testability*
6. *Scalability*

### 5.What is a Dependency?
-In Java, a dependency refers to a situation where one class, module, or component relies on another class, module, or component in some way. 
- Dependencies are a fundamental concept in object-oriented programming and software design, and they represent the relationships and interactions between various parts of a Java program.
- There are different types of dependencies in Java:
1. *Compile-Time Dependencies*
2. *Run-Time Dependencies*
3. *Transitive Dependencies*

### 6.What Is a Spring Bean?
- Here’s a definition of beans in the Spring Framework documentation: \
  In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container.
- Any normal Java POJO class can be a Spring Bean if it’s configured to be initialized via container by providing configuration metadata information.

-----
*Example to understand topic easily*

Assume we have a class declaration:

```
public class Company {
    private Address address;

    public Company(Address address) {
        this.address = address;
    }

    // getter, setter and other properties
}
```
This class needs a collaborator of type Address
```
public class Address {
    private String street;
    private int number;

    public Address(String street, int number) {
        this.street = street;
        this.number = number;
    }

    // getters and setters
}
```
**Traditional Approach**

Normally, we create objects with their classes’ constructors:
```
Address address = new Address("High Street", 1000);
Company company = new Company(address);
```
There’s nothing wrong with this approach, but wouldn’t it be nice to manage the dependencies in a better way? \
Imagine an application with dozens or even hundreds of classes. \
Sometimes we want to share a single instance of a class across the whole application, other times we need a separate object for each use case, and so on. \
Managing such a number of objects is nothing short of a nightmare.This is where inversion of control comes to the rescue. \
Instead of constructing dependencies by itself, an object can retrieve its dependencies from an IoC container. \
All we need to do is to provide the container with appropriate configuration metadata.

**IOC in Action**

*Bean Configuration*
First off, let’s decorate the Company class with the @Component annotation:
```
@Component
public class Company {
    // this body is the same as before
}
```

Here’s a configuration class supplying bean metadata to an IoC container:

```
@Configuration
@ComponentScan(basePackageClasses = Company.class)
public class Config {
    @Bean
    public Address getAddress() {
        return new Address("High Street", 1000);
    }
}
```
The configuration class produces a bean of type Address. It also carries the @ComponentScan annotation, which instructs the container to look for beans in the package containing the Company class.
When a Spring IoC container constructs objects of those types, all the objects are called Spring beans, as they are managed by the IoC container.
Since we defined beans in a configuration class, we’ll need an instance of the AnnotationConfigApplicationContext class to build up a container:
```
ApplicationContext context = new AnnotationConfigApplicationContext(Config.class);
```
A quick test verifies the existence and the property values of our beans:
```
Company company = context.getBean("company", Company.class);
assertEquals("High Street", company.getAddress().getStreet());
assertEquals(1000, company.getAddress().getNumber());
```
The result proves that the IoC container has created and initialized beans correctly.

------

### 7.How to create/register a Spring bean?
Spring Framework provides three ways to configure beans to be used in the application. \
*Annotation Based Configuration* - By using @Service or @Component annotations. Scope details can be provided with @Scope annotation.\
*XML Based Configuration* - By creating Spring Configuration XML file to configure the beans. If you are using Spring MVC framework, the xml based configuration can be loaded automatically by writing some boiler plate code in web.xml file. \
*Java Based Configuration* - Starting from Spring 3.0, we can configure Spring beans using java programs. Some important annotations used for java based configuration are @Configuration, @ComponentScan and @Bean.

- When using @Bean, you have to register the bean explicitly in a configuration class.
- When using @Controller, @Service, or @Repository, Spring will automatically detect and register those annotated classes as beans during component scanning, and you don't need to provide separate bean registrations.

-----
*Example to understand topic easily* 

**Annotation Based Spring Bean Configuration**

```
package com.journaldev.spring.beans;

import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Service;
import org.springframework.web.context.WebApplicationContext;

@Service
@Scope(WebApplicationContext.SCOPE_REQUEST)
public class MyAnnotatedBean {

	private int empId;

	public int getEmpId() {
		return empId;
	}

	public void setEmpId(int empId) {
		this.empId = empId;
	}
	
}
```
MyAnnotatedBean is configured using *@Service* and scope is set to *Request*.

*Spring IoC Controller Class*

HomeController class will handle the HTTP requests for the home page of the application. We will inject our Spring beans to this controller class through WebApplicationContext container.
```
package com.journaldev.spring.controller;

import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import com.journaldev.spring.beans.MyAnnotatedBean;
import com.journaldev.spring.beans.MyBean;

@Controller
@Scope("request")
public class HomeController {
		
	private MyBean myBean;
	
	private MyAnnotatedBean myAnnotatedBean;

	@Autowired
	public void setMyBean(MyBean myBean) {
		this.myBean = myBean;
	}

	@Autowired
	public void setMyAnnotatedBean(MyAnnotatedBean obj) {
		this.myAnnotatedBean = obj;
	}
	
	/**
	 * Simply selects the home view to render by returning its name.
	 */
	@RequestMapping(value = "/", method = RequestMethod.GET)
	public String home(Locale locale, Model model) {
		System.out.println("MyBean hashcode="+myBean.hashCode());
		System.out.println("MyAnnotatedBean hashcode="+myAnnotatedBean.hashCode());
		
		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
		
		String formattedDate = dateFormat.format(date);
		
		model.addAttribute("serverTime", formattedDate );
		
		return "home";
	}
	
}
```
Now when you will launch the web application, the home page will get loaded and in the console following logs will be printed when you refresh the page multiple times.

Output:
```
MyBean hashcode=118267258
MyAnnotatedBean hashcode=1703899856
MyBean hashcode=118267258
MyAnnotatedBean hashcode=1115599742
MyBean hashcode=118267258
MyAnnotatedBean hashcode=516457106
```
Notice that MyBean is configured to be a singleton, so the container is always returning the same instance and hashcode is always the same. Similarly, for each request, a new instance of MyAnnotatedBean is created with different hashcode.

**XML Based Spring Bean Configuration**

MyBean is a simple Java POJO class.
```
package com.journaldev.spring.beans;

public class MyBean {

	private String name;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
}
```

Spring Configuration XML File
servlet-context.xml code:
```
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="https://www.springframework.org/schema/mvc"
	xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
	xmlns:beans="https://www.springframework.org/schema/beans"
	xmlns:context="https://www.springframework.org/schema/context"
	xsi:schemaLocation="https://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd
		https://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
		https://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

	<!-- DispatcherServlet Context: defines this servlet's request-processing infrastructure -->
	
	<!-- Enables the Spring MVC @Controller programming model -->
	<annotation-driven />

	<!-- Handles HTTP GET requests for /resources/** by efficiently serving up static resources in the ${webappRoot}/resources directory -->
	<resources mapping="/resources/**" location="/resources/" />

	<!-- Resolves views selected for rendering by @Controllers to .jsp resources in the /WEB-INF/views directory -->
	<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/" />
		<beans:property name="suffix" value=".jsp" />
	</beans:bean>
	
	<context:component-scan base-package="com.journaldev.spring" />
	
	<beans:bean name="myBean" class="com.journaldev.spring.beans.MyBean" scope="singleton" ></beans:bean>
	
</beans:beans>
```
Notice that MyBean is configured using bean element with scope as singleton.

**Java Based Spring Bean Configuration**

For standalone applications, we can use annotation based as well as XML based configuration. The only requirement is to initialize the context somewhere in the program before we use it.
```
package com.journaldev.spring.main;

import java.util.Date;

public class MyService {

	public void log(String msg){
		System.out.println(new Date()+"::"+msg);
	}
}
```
MyService is a simple java class with some methods.
```
package com.journaldev.spring.main;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(value="com.journaldev.spring.main")
public class MyConfiguration {

	@Bean
	public MyService getService(){
		return new MyService();
	}
}
```
The annotation based configuration class that will be used to initialize the Spring container.
```
package com.journaldev.spring.main;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MyMainClass {

	public static void main(String[] args) {
		
		AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(
				MyConfiguration.class);
		MyService service = ctx.getBean(MyService.class);
		
		service.log("Hi");
		
		MyService newService = ctx.getBean(MyService.class);
		System.out.println("service hashcode="+service.hashCode());
		System.out.println("newService hashcode="+newService.hashCode());
		ctx.close();
	}

}
```
A simple test program where we are initializing the AnnotationConfigApplicationContext context and then using getBean() method to get the instance of MyService. Notice that I am calling getBean method two times and printing the hashcode. Since there is no scope defined for MyService, it should be a singleton and hence hashcode should be the same for both the instances. When we run the above application, we get following console output confirming our understanding.

Output:
```
Sat Dec 28 22:49:18 PST 2013::Hi
service hashcode=678984726
newService hashcode=678984726
```

- *Points to remember*
- If you're using @Bean to define beans in a configuration class, you do need the configuration class. In this case, the configuration class serves as a central place to define and configure your beans. It's a common approach for customizing bean creation and wiring.
- When you use annotations like @Service, @Controller, or @Repository, you typically don't need a separate configuration class. Component scanning, enabled through @ComponentScan, automatically detects and registers classes with these annotations as Spring beans. Component scanning simplifies bean registration without requiring explicit configurations.

---
### 8.How to Define the Scope of a Bean?
- In *XML Based Spring Bean Configuration*,Scope is defined as 
```
<bean id = "..." class = "..." scope = "singleton">
   <!-- collaborators and configuration for this bean go here -->
</bean>
```
- In *Annotation Based Spring Bean Configuration*,scope is defined with @Scope annotation on @Service or @Component class
```
@Service
@Scope("singleton")
public class ServiceClass {
}
```
- In *Java Based Spring Bean Configuration* ,scope is defibed with @Scope annotation on @Configuration,@Bean.
```
@Configuration
public class MyConfiguration {
	
	@Bean
	@Scope(value="singleton")
    public MyBean myBean() {
		return new MyBean();
	}
	
}
```
### 9.What Is the Default Bean Scope in Spring Framework?
- Singleton scope is the default scope in Spring Framework.

### 10.What are the other scopes available?
There are five scopes defined for Spring Beans.
- *singleton* - Only one instance of the bean will be created for each container. This is the default scope for the spring beans. While using this scope, make sure bean doesn’t have shared instance variables otherwise it might lead to data inconsistency issues.(refer ans to que.12)
- *prototype* - A new instance will be created every time the bean is requested.
- *request* - This is same as prototype scope, however it’s meant to be used for web applications. A new instance of the bean will be created for each HTTP request.
- *session* - A new bean will be created for each HTTP session by the container.
- *global-session* - This is used to create global session beans for Portlet applications.
Spring Framework is extendable and we can create our own scopes too. However, most of the times we are good with the scopes provided by the framework.

### 11.How is Spring’s singleton bean different from Gang of Four Singleton Pattern?
- GOF Singleton Pattern as per Wikipedia
> A Java singleton, per the design pattern where instantiation is restricted to one, usually per class loader by the code.
- Spring Singleton as per Spring 3.1 Doc
> A Spring singleton bean can be any normal class you write, but declaring it's scope as singleton means that Spring will only create one instance and provide its reference to all beans that reference the declared bean. You may have many instances of that class in your application, but only one will be created for that bean. You may even have multiple beans of the same class all declared as singleton. Each bean will create exactly one instance of the class.
- The *Java singleton Pattern* is scoped by the Java class loader, the *Spring singleton* is scoped by the container context.
Which basically means that,
- In Java, you can be sure that a singleton is a truly a singleton only within the context of the class loader which loaded it. Other class loaders should be capable of creating another instance of it (provided the class loaders are not in the same class loader hierarchy), despite of all your efforts in code to try to prevent it.
- In Spring, if you could load your singleton class in two different contexts and then again we can break the singleton concept.
- So, in summary, Java considers something a singleton if it cannot create more than one instance of that class within a given class loader, whereas Spring would consider something a singleton if it cannot create more than one instance of a class within a given container context.
- Even if we declare same bean two different times, it will be created just once. Spring is smart enough to handle that and when you try to fetch instances via IDs, can be tested using "==" operator.

### 12.Are Singleton Beans Thread-Safe?
- No. The two concepts are not even related.
- Singletons are about *creation*. This design pattern ensures that only one instance of a class is created.Thread safety is about *execution*. To quote Wikipedia:
> A piece of code is thread-safe if it only manipulates shared data structures in a manner that guarantees safe execution by multiple threads at the same time.
- So eventually thread safety depends on the code and the code only. And this is the reason why Spring beans are not thread safe per se.
- Spring singleton beans are created once and there can be only one instance available at any point of time.
- Lets say your have an instance variable which is modified in an non-synchronized method. \
  In multi-threaded environment,same class instance will be assigned to all the threads and 2 concurrent threads can update/change the instance variables which may lead unexpected situation. \
  Singleton beans does not provide thread safety and now you know that instance variables usage may lead to unexpected result, you have 2 options to solve the same :
1. Don't use instance variables in multithreaded environment. OR
2. Use synchronized block/keyword on methods wherever the instance variables are modified to avoid unexpected results.

### 13.What Does the Spring Bean Lifecycle Look Like?
- The bean life cycle refers to when & how the bean is instantiated, what action it performs until it lives, and when & how it is destroyed.
- Bean life cycle is managed by the spring container.
- When we run the program then, first of all,
  1. the spring container gets started.
  2. After that, the container creates the instance of a bean as per the request,
  3. Dependencies are injected.
  4. Custom init() method is called. \
     if we want to execute some code on the bean instantiation then we can write that code inside the custom init() method.
  5. Custom utility methods are called.
  6. Custom destroy() is called. \
     if we want to execute some code just after closing the spring container then we can write that code inside the destroy() method.
  7. And finally, the bean is destroyed when the spring container is closed.
- Note: We can choose a custom method name instead of init() and destroy().
  
The following image shows the process flow of the bean life cycle.(Soure : Geeksforgeeks)
![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20200428011831/Bean-Life-Cycle-Process-flow3.png)

### 14.What is the difference between XML based and Java based Configurations for Spring?
1. **Configuration Style**:
- *XML Configuration*: In XML configuration, you define beans and their dependencies using XML files. You configure the application context and bean definitions in XML files.
- *Java Configuration*: In Java configuration, you use Java classes annotated with @Configuration to define beans and their relationships. You write Java code to configure the application context.
2. **Readability**:
- *XML Configuration*: XML configuration can be verbose and less readable, especially for complex applications with numerous beans and dependencies. XML files tend to be larger and may require more effort to understand.
- *Java Configuration*: Java configuration tends to be more concise and readable. It leverages the features of the Java language, including method calls and annotations, which can make the configuration more intuitive and easier to follow.
3. **Annotating Components**:
- *XML Configuration*: In XML, you typically use the <bean> element to define beans. You don't use annotations like @Component, @Service, @Repository, etc., unless you explicitly enable component scanning.
- *Java Configuration*: In Java configuration, you often use annotations like @Component, @Service, @Repository, and @Configuration to mark and define beans. Component scanning is more commonly used in Java configuration.

### 15.How do you choose between XML and Java Configurations for Spring?
- Java based configuration have benefits of xml based configuration due to below reasons:
1. *Type Safety*: Java-based configurations are written in Java code, which is statically typed. This means that the compiler can catch type-related errors at compile time, providing better type safety. In contrast, XML configurations are inherently dynamic and can only be validated at runtime.
2. *Easy to maintain*: XML based on configuration can quickly grow big. [Yes we can split and import but still]
3. *Refactoring*: When you refactor your code, such as renaming a class or package, Java-based configurations are automatically updated by the IDE, ensuring that your configuration remains in sync with your code. In XML configurations, you would need to manually update references, which can lead to errors.
4. *Conditional Configuration*: Java-based configurations allow you to use conditional logic to configure beans based on specific conditions, such as the presence of certain properties or environment variables. This flexibility is challenging to achieve with XML.

### 16.How do you define a component scan in XML and Java Configurations?
**XML Configuration**:
- In XML-based configuration, you typically define component scanning using the <context:component-scan> element within your Spring application context XML file. Here's an example:
```
<context:component-scan base-package="com.example.myapp" />
```
In this example, the base-package attribute specifies the base package(s) to scan for components. Spring will scan all classes in the specified package(s) and its sub-packages for classes annotated with annotations like @Component, @Service, @Repository, and @Controller. These annotated classes will be automatically registered as Spring beans.

**Java Configuration (using @ComponentScan)**: 
- In Java-based configuration, you can use the @ComponentScan annotation to achieve the same result. Here's an example:
```
@Configuration
@ComponentScan(basePackages = "com.example.myapp")
public class AppConfig {
    // Additional configuration and bean definitions can be placed here
}
```
This Java configuration class is annotated with @Configuration and @ComponentScan, specifying the base package to scan for components.

### 17.What is IOC (Inversion of Control)?
- Inversion of Control is a principle in software engineering which transfers the control of objects or portions of a program to a container or framework, often used it in the context of object-oriented programming.
- In contrast with traditional programming, in which our custom code makes calls to a library, IoC enables a framework to take control of the flow of a program and make calls to our custom code. To enable this, frameworks use abstractions with additional behavior built in. If we want to add our own behavior, we need to extend the classes of the framework or plugin our own classes.
- The advantages of this architecture are:
1. decoupling the execution of a task from its implementation
2. making it easier to switch between different implementations
3. greater modularity of a program
4. greater ease in testing a program by isolating a component or mocking its dependencies, and allowing components to communicate through contracts
- We can achieve Inversion of Control through various mechanisms such as: \
Strategy design pattern, Service Locator pattern, Factory pattern, and Dependency Injection (DI).

### 18.What is IOC Container & it's important roles?
- Spring IoC (Inversion of Control) Container is the core of Spring Framework.
- It creates the objects, configures and assembles their dependencies, manages their entire life cycle.
- The Container uses Dependency Injection(DI) to manage the components that make up the application.
- It gets the information about the objects from a configuration file(XML)[XML based bean configuration] or Java Code[Java based bean configuration] or Java Annotations[Annotation based bean configuration] and Java POJO class. These objects are called *Beans*.
- Since the Controlling of Java objects and their lifecycle is not done by the developers, hence the name *Inversion Of Control*.
- There are 2 types of IoC containers:
  1. BeanFactory 
  2. ApplicationContext 
- That means if you want to use an IoC container in spring whether we need to use a *BeanFactory* or *ApplicationContext*. The BeanFactory is the most basic version of IoC containers, and the ApplicationContext extends the features of BeanFactory.
- The followings are some of the features/roles of Spring IoC,
  1. Creating Object for us,
  2. Managing our objects,
  3. Helping our application to be configurable,
  4. Managing dependencies
  5. Managing bean entire life cycle.

-----
*Example to understand topic easily* 

Let’s understand what is IoC in Spring with an example. Suppose we have one interface named Sim and it has some abstract methods calling() and data().
```
// Java Program to Illustrate Sim Interface
public interface Sim
{
    void calling();
    void data();
}
```
Now we have created another two classes Airtel and Jio which implement the Sim interface and override the interface methods.
```
// Java Program to Illustrate Airtel Class
 
// Class
// Implementing Sim interface
public class Airtel implements Sim {
 
    @Override public void calling()
    {
        System.out.println("Airtel Calling");
    }
 
    @Override public void data()
    {
        System.out.println("Airtel Data");
    }
}
```

```
// Java Program to Illustrate Jio Class
 
// Class
// Implementing Sim interface
public class Jio implements Sim{
    @Override
    public void calling() {
        System.out.println("Jio Calling");
    }
 
    @Override
    public void data() {
        System.out.println("Jio Data");
    }
}
```

So let’s now call these methods inside the main method. So by implementing the Run time polymorphism concept we can do something like this

```
// Java Program to Illustrate Mobile Class
 
// Class
public class Mobile {
 
    // Main driver method
    public static void main(String[] args)
    {
 
        // Creating instance of Sim interface
        // inside main() method
        // with reference to Jio class constructor
        // invocation
        Sim sim = new Jio();
 
        // Sim sim = new Airtel();
 
        sim.calling();
        sim.data();
    }
}
```
But what happens if in the future another new Sim Vodafone came and we need to change again to the child class name in the code, like this
```
Sim sim = new Vodafone();
```
So we have to do our configuration in the source code. So how to make it configurable? \
We don’t want to touch the source code of this. The source code should be constant. \
And how can we make it? \
Here Spring IoC comes into the picture. So in this example, we are going to use *ApplicationContext* to implement an IoC container. \

First, we have to create an XML file and name the file as “beans.xml“.

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd">
 
  <bean id="sim" class="Jio"></bean>
</beans>
```

Output Explanation: 
In the beans.xml file, we have created beans. So inside the id, we have to pass the unique id and inside the class, we have to pass the Class name for which you want to create the bean. Later on, inside the main method, we can tweek it out that will be described in the upcoming program.

> Bean Definition: In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container.
```
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
 
public class Mobile {
    public static void main(String[] args) {
        // Using ApplicationContext tom implement Spring IoC
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
         
        // Get the bean
        Sim sim = applicationContext.getBean("sim", Sim.class);
         
        // Calling the methods
        sim.calling();
        sim.data();
    }
}
```
Output:
```
Jio Calling
Jio Data
```
And now if you want to use the Airtel sim so you have to change only inside the beans.xml file. The main method is going to be the same.
```
<bean id="sim" class="Airtel"></bean>
```

```
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
 
public class Mobile {
    public static void main(String[] args) {
       
        // Using ApplicationContext tom implement Spring IoC
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
         
        // Get the bean
        Sim sim = applicationContext.getBean("sim", Sim.class);
         
        // Calling the methods
        sim.calling();
        sim.data();
    }
}
```
Output:
```
Airtel Calling
Airtel Data
```
------
### 19.What is Bean Factory?
- The BeanFactory is the actual container which instantiates, configures, and manages a number of beans.
- These beans typically collaborate with one another, and thus have dependencies between themselves.
- These dependencies are reflected in the configuration data used by the BeanFactory (although some dependencies may not be visible as configuration data, but rather be a function of programmatic interactions between beans at runtime).
- A BeanFactory is represented by the interface org.springframework.beans.factory.BeanFactory, for which there are multiple implementations.
- The most commonly used simple BeanFactory implementation is org.springframework.beans.factory.xml.XmlBeanFactory. (This should be qualified with the reminder that ApplicationContexts are a subclass of BeanFactory, and most users end up using XML variants of ApplicationContext).
- Although for most scenarios, almost all user code managed by the BeanFactory does not have to be aware of the BeanFactory, the BeanFactory does have to be instantiated somehow. This can happen via explicit user code such as:
```
Resource res = new FileSystemResource("beans.xml");
XmlBeanFactory factory = new XmlBeanFactory(res);
```
or
```
ClassPathResource res = new ClassPathResource("beans.xml");
XmlBeanFactory factory = new XmlBeanFactory(res);
```
or
```
ClassPathXmlApplicationContext appContext = new ClassPathXmlApplicationContext(
        new String[] {"applicationContext.xml", "applicationContext-part2.xml"});
// of course, an ApplicationContext is just a BeanFactory
BeanFactory factory = (BeanFactory) appContext;
```
----
*Example to understand topic easily* 

Bean Definition: Create a Student POJO class.
```
// Java Program where we are creating a POJO class

// POJO class
public class Student {

  // Member variables
  private String name;
  private String age;

  // Constructor 1
  public Student() {
  }

  // Constructor 2
  public Student(String name, String age) {
    this.name = name;
    this.age = age;
  }

  // Method inside POJO class
  @Override
  public String toString() {

    // Print student class attributes
    return "Student{" + "name='" + name + '\'' + ", age='" + age + '\'' + '}';
  }
}
```
XML Bean Configuration: Configure the Student bean in the bean-factory-demo.xml file.
```
<?xml version = "1.0" encoding="UTF-8"?>
<beans xmlns = "http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation = "http://www.springframework.org/schema/beans
            https://www.springframework.org/schema/beans/spring-beans.xsd">
            
    <bean id="student" class = "com.gfg.demo.domain.Student">
                <constructor-arg name="name" value="Tina"/>
                <constructor-arg name="age" value="21"/>
        </bean>
</beans>
```
Main Class
```
// Application class 
@SpringBootApplication

// Main class
public class DemoApplication {

  // Main driver method
  public static void main(String[] args) {

    // Creating object in a spring container (Beans)
    BeanFactory factory = new ClassPathXmlApplicationContext("bean-factory-demo.xml");
    Student student = (Student) factory.getBean("student");

    System.out.println(student);
  }
}
```
Output:
```
Student{name='Tina', age='21'}
```
*Note: XmlBeanFactory class is deprecated.*

-----

###  20.What is Application Context?
- ApplicationContext is the sub-interface of BeanFactory.
- BeanFactory provides basic functionalities and is recommended to use for lightweight applications like mobile and applets.
- ApplicationContext provides basic features in addition to enterprise-specific functionalities which are as follows:
1. Publishing events to registered listeners by resolving property files.
2. Methods for accessing application components.
3. Supports Internationalization.
4. Loading File resources in a generic fashion.
Note: It is because of these additional features, developers prefer to use ApplicationContext over BeanFactory. 

*ApplicationContext Implementation Classes*
- There are different types of Application containers provided by Spring for different requirements as listed below which later onwards are described alongside with declaration, at lastly providing an example to get through the implementation part with the pictorial aids. Containers are as follows:
1. AnnotationConfigApplicationContext container 
2. AnnotationConfigWebApplicationContext
3. XmlWebApplicationContext
4. FileSystemXmlApplicationContext
5. ClassPathXmlApplicationContext

-----
*Detailed Explanation for better understanding*

**Container 1: AnnotationConfigApplicationContext**

*Use*: This class is used to create a Spring application context based on Java-based configuration classes annotated with annotations like @Configuration.Typical *Scenario*: When you prefer configuring your Spring application using Java-based configuration and annotations rather than XML.\
For example, in the below declaration, two Configuration classes Appconfig and AppConfig1 are passed as arguments to the constructor. The beans defined in later classes will override the same type and name beans in earlier classes when passed as arguments. \
For example, AppConfig and AppConfig1 have the same bean declaration. The bean defined in AppConfig1 overrides the bean in AppConfig.

Syntax: Declaration
```
ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class, AppConfig1.class);
```
Note: Add the following to the properties file in the IDE to allow the spring to override beans.
```
spring.main.allow-bean-definition-overriding=true
```

**Container 2: AnnotationConfigWebApplicationContext**

*Use*: Similar to AnnotationConfigApplicationContext, this class is designed for web applications and is often used in a Spring MVC environment. It can be configured using Java-based configuration for the web layer.
*Typical Scenario*: When you're building a web application and want to use Java-based configuration for your Spring MVC components.
 ```
// Class
// Implementing WebApplicationInitializer
public class MyWebApplicationInitializer implements WebApplicationInitializer {

  // Servlet container

  public void onStartup(ServletContext container) throws ServletException {
    AnnotationConfigWebApplicationContext context = new AnnotationConfigWebApplicationContext();
    context.register(AppConfig.class);
    context.setServletContext(container);

    // Servlet configuration
  }
}
```

**Container 3: XmlWebApplicationContext**

*Use*: This class is used to create a Spring application context based on XML configuration files specifically tailored for web applications. It can load configuration from web-specific XML files.
*Typical Scenario*: When you're working on a web application and prefer to configure your Spring context using XML files designed for web-related settings, like servlet mappings and web-specific beans.
```
// Class
// Implementing WebApplicationInitializer
public class MyXmlWebApplicationInitializer implements WebApplicationInitializer {

  // Servlet container
  public void onStartup(ServletContext container) throws ServletException {
    XmlWebApplicationContext context = new XmlWebApplicationContext();
    context.setConfigLocation("/WEB-INF/spring/applicationContext.xml");
    context.setServletContext(container);

    // Servlet configuration
  }
}
```

**Container 4: FileSystemXmlApplicationContext**

*Use*: This class creates a Spring application context based on XML configuration files located in the file system. You specify the file path(s) to the XML configuration files.
*Typical Scenario*: When you need to load Spring configuration from XML files stored on the local file system rather than from the classpath. This is less common in modern applications, as most configurations are bundled with the application.

Illustration:
```
String path = "Documents/demoProject/src/main/resources/applicationcontext/student-bean-config.xml";

ApplicationContext context = new FileSystemXmlApplicationContext(path);
AccountService accountService = context.getBean("studentService", StudentService.class);
```

**Container 5: ClassPathXmlApplicationContext**

*Use*: This class is used to create a Spring application context based on XML configuration files located on the classpath. You specify the classpath resource location(s) for the XML files.
*Typical Scenario*: When your Spring application relies on XML-based configuration and you want to load configuration files from the classpath. This is a common choice for traditional Spring applications using XML configuration.

Illustration:
```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationcontext/student-bean-config.xml");
StudentService studentService = context.getBean("studentService", StudentService.class);
```
----

### Can you compare Bean Factory with Application Context?
|            BeanFactory 	 			|         ApplicationContext 			|
| ---------------------------------     | ---------------------------------     |
| It is a fundamental container that provides the basic functionality for extends the BeanFactory that managing beans. | It is an advanced container that extends the BeanFactory that provides all basic functionality and adds some advanced features. |
| It is suitable to build standalone applications. | It is suitable to build Web applications, integration with AOP modules, ORM and distributed applications. |
| It supports only Singleton and Prototype bean scopes. | It supports all types of bean scopes such as Singleton, Prototype, Request, Session etc. |
| It does not support Annotations. In Bean Autowiring, we need to configure the properties in XML file only. | It supports Annotation based configuration in Bean Autowiring. |
| This interface does not provides messaging (i18n or internationalization) functionality. | ApplicationContext interface extends MessageSource interface, thus it provides messaging (i18n or internationalization) functionality. |
| BeanFactory does not support Event publication functionality. | Event handling in the ApplicationContext is provided through the ApplicationEvent class and ApplicationListener interface. |
| In BeanFactory, we need to manually register BeanPostProcessors and BeanFactoryPostProcessors. | The ApplicationContext automatically registers BeanFactoryPostProcessor and BeanPostProcessor at startup. |
| BeanFactory will create a bean object when the getBean() method is called thus making it Lazy initialization. | ApplicationContext loads all the beans and creates objects at the time of startup only thus making it Eager initialization. |
| BeanFactory interface provides basic features only thus requires less memory. For standalone applications where the basic features are enough and when memory consumption is critical, we can use BeanFactory. | ApplicationContext provides all the basic features and advanced features, including several that are geared towards enterprise applications thus requires more memory. |

For more info refer <a href="https://www.geeksforgeeks.org/spring-difference-between-beanfactory-and-applicationcontext/" target="_blank">gfg</a>

### 21.How do you create an application context with Spring?
- refer space between que.18 and 19

### 22.What are the different options available to create Application Contexts for Spring?
- refer que.20

### 23.How does Spring know where to search for Components or Beans?
- Where to search for the beans is defined by the @ComponentScan which can be annotated on the @Configuration class that is used to bootstrap Spring.
- For example , it has an attribute called scanBasePackages which tells Spring to scan the beans(A class that is annotated with @Component or its sterotypes such as @Service , @Repository , @Controller etc. ) from certain packages and its sub-packages only.
- Then for each bean that are registered , it goes on see if there are any methods annotation with @Bean.If yes, also register them as beans.

-----
*long answer for better understanding*

**@ComponentScan**
If you understand Component Scan, you understand Spring.

Spring is a dependency injection framework. It is all about beans and wiring in dependencies. \
The first step of defining Spring Beans is by adding the right annotation — @Component or @Service or @Repository. \
However, Spring does not know about the bean unless it knows where to search for it. \
This part of “telling Spring where to search” is called a **Component Scan**. \
You define the packages that have to be scanned.

Once you define a Component Scan for a package, Spring would search the package and all its sub packages for components/beans.

*Defining a Component Scan*

If you are using Spring Boot, check the configuration in Approach 1.
If you are doing a JSP/Servlet or a Spring MVC application without using Spring Boot, use Approach 2.

*Approach 1: Component Scan in a Spring Boot Project*

If your other package hierarchies are below your main app with the @SpringBootApplication annotation, you’re covered by the implicit Component Scan. If there are beans/components in other packages that are not sub-packages of the main package, you should manually add them as @ComponentScan.

Consider below class
```
package com.in28minutes.springboot.basics.springbootin10steps;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ConfigurableApplicationContext;
@SpringBootApplication
public class SpringbootIn10StepsApplication {
    public static void main(String[] args) {
        ApplicationContext applicationContext =
            SpringApplication.run(SpringbootIn10StepsApplication.class, args);
        for (String name: applicationContext.getBeanDefinitionNames()) {
            System.out.println(name);
        }
    }
}
```
*@SpringBootApplication* is defined in the SpringbootIn10StepsApplication class which is in the package com.in28minutes.springboot.basics.springbootin10steps \
@SpringBootApplication defines an automatic Component Scan on the package com.in28minutes.springboot.basics.springbootin10steps. \
You are fine if all your components are defined in the above package or a sub-package of it. \

However, let’s say one of the components is defined in package com.in28minutes.springboot.somethingelse \
In this case, you would need to add the new package into Component Scan. \

You have two options:

Option 1:
```
@ComponentScan(“com.in28minutes.springboot”)
@SpringBootApplication
public class SpringbootIn10StepsApplication {...}
```
Option 2:: Define as array
```
@ComponentScan({"com.in28minutes.springboot.basics.springbootin10steps","com.in28minutes.springboot.somethingelse"})
@SpringBootApplication
public class SpringbootIn10StepsApplication {...}
```

*Approach 2: Non-Spring Boot Project*

Option 1:
```
@ComponentScan(“com.in28minutes)
@Configuration
public class SpringConfiguration {...}
```
Option 2:
```
@ComponentScan({"com.in28minutes.package1","com.in28minutes.package2"})
@Configuration
public class SpringConfiguration {...}
```
XML application context:
```
<context:component-scan base-package="com.in28minutes" />
```
Specific multiple packages:
```
<context:component-scan base-package="com.in28minutes.package1, com.in28minutes.package2" 
```
-----

### 24.What is Dependency Injection?
- Dependency injection (DI) is a process whereby objects define their dependencies (that is, the other objects with which they work) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method.
- The container then injects those dependencies when it creates the bean.
- This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies on its own by using direct construction of classes or the Service Locator pattern.

### 25.What is setter injection?
- For setter-based DI, the container will call setter methods of our class after invoking a no-argument constructor or no-argument static factory method to instantiate the bean.
- Let’s create this configuration using annotations:
```
@Bean
public Store store() {
    Store store = new Store();
    store.setItem(item1());
    return store;
}
```
- We can also use XML for the same configuration of beans:
```
<bean id="store" class="org.baeldung.store.Store">
    <property name="item" ref="item1" />
</bean>
```
We can combine constructor-based and setter-based types of injection for the same bean. The Spring documentation recommends using constructor-based injection for mandatory dependencies, and setter-based injection for optional ones.

### 26.What is constructor injection?
- In the case of constructor-based dependency injection, the container will invoke a constructor with arguments each representing a dependency we want to set.
- Spring resolves each argument primarily by type, followed by name of the attribute, and index for disambiguation.
- Let’s see the configuration of a bean and its dependencies using annotations:
```
@Configuration
public class AppConfig {

    @Bean
    public Item item1() {
        return new ItemImpl1();
    }

    @Bean
    public Store store() {
        return new Store(item1());
    }
}
```
- The @Configuration annotation indicates that the class is a source of bean definitions. We can also add it to multiple configuration classes.
- We use the @Bean annotation on a method to define a bean. If we don’t specify a custom name, then the bean name will default to the method name.
- For a bean with the default singleton scope, Spring first checks if a cached instance of the bean already exists, and only creates a new one if it doesn’t. If we’re using the prototype scope, the container returns a new bean instance for each method call.
- Another way to create the configuration of the beans is through XML configuration:
```
<bean id="item1" class="org.baeldung.store.ItemImpl1" /> 
<bean id="store" class="org.baeldung.store.Store"> 
    <constructor-arg type="ItemImpl1" index="0" name="item" ref="item1" /> 
</bean>
```

### 27.Which Is the Best Way of Injecting Beans and Why?
1. *All Required Dependencies Are Available at Initialization Time* - \
We create an object by calling a constructor. 
If the constructor expects all required dependencies as parameters,then we can be 100% sure that the class will never be instantiated without its dependencies injected.
The IoC container makes sure that all the arguments provided in the constructor are available before passing them into the constructor.
This helps in preventing the infamous NullPointerException.
Constructor injection is extremely useful since we do not have to write separate business logic everywhere to check if all the required dependencies are loaded, 
thus simplifying code complexity.

- What About Optional Dependencies? \
With setter injection, Spring allows us to specify optional dependencies by adding @Autowired(required = false) to a setter method.
This is not possible with constructor injection since the required=false would be applied to all constructor arguments.
We can still provide optional dependencies with constructor injection using Java's Optional type.

2. *Identifying Code Smells* - \
Constructor injection helps us to identify if our bean is dependent on too many other objects. 
If our constructor has a large number of arguments this may be a sign that our class has too many responsibilities. 
We may want to think about refactoring our code to better address proper separation of concerns.

3. *Preventing Errors in Tests* - \
Constructor injection simplifies writing unit tests. 
The constructor forces us to provide valid objects for all dependencies. 
Using mocking libraries like Mockito, we can create mock objects that we can then pass into the constructor.
We can also pass mocks via setters, of course, but if we add a new dependency to a class, we may forget to call the setter in the test, potentially causing a NullPointerException in the test.
Constructor injection ensures that our test cases are executed only when all the dependencies are available. 
It’s not possible to have half created objects in unit tests (or anywhere else for that matter).

4. *Immutability* - \
Constructor injection helps in creating immutable objects because a constructor’s signature is the only possible way to create objects. 
Once we create a bean, we cannot alter its dependencies anymore. 
With setter injection, it’s possible to inject the dependency after creation, thus leading to mutable objects which, among other things, may not be thread-safe in a multi-threaded environment and are harder to debug due to their mutability.

### 28.What is Auto Wiring in Spring?
- Wiring allows the Spring container to automatically resolve dependencies between collaborating beans by inspecting the beans that have been defined.
- The Spring container detects those dependencies specified in the configuration file and @ the relationship between the beans. This is referred to as autowiring in Spring.
- An autowired application requires fewer lines of code comparatively but at the same time, it provides very little flexibility to the programmer.
  
### 29.What are the different modes of Autowiring in Spring?
- *No autowiring*: In this mode, you need to explicitly wire the bean properties using the <ref/> element in XML configuration or @Bean methods in Java-based configuration. \
XML Configuration:
```
<bean id="myBean" class="com.example.MyBean">
    <property name="myDependency" ref="myDependencyBean"/>
</bean>
<bean id="myDependencyBean" class="com.example.MyDependency"/>
```
Java-based Configuration:
```
@Configuration
public class MyConfig {
    @Bean
    public MyBean myBean() {
        MyBean bean = new MyBean();
        bean.setMyDependency(myDependency());
        return bean;
    }

    @Bean
    public MyDependency myDependency() {
        return new MyDependency();
    }
}
```

- *Autowiring by name*: In this mode, properties of the autowired bean are wired by searching for a bean with the same name or ID in the configuration file. \
XML Configuration:
```
<bean id="myBean" class="com.example.MyBean" autowire="byName"/>
<bean id="myDependency" class="com.example.MyDependency"/>
```
Java-based Configuration:
```
@Configuration
public class MyConfig {
    @Autowired
    private MyDependency myDependency;

    @Bean
    public MyBean myBean() {
        return new MyBean();
    }

    @Bean
    public MyDependency myDependency() {
        return new MyDependency();
    }
}
```
- *Autowiring by type*: In this mode, properties of the autowired bean are wired by searching for a bean whose type is compatible with the property’s type. \
XML Configuration:
```
<bean id="myBean" class="com.example.MyBean" autowire="byType"/>
<bean id="myDependency" class="com.example.MyDependency"/>
```
Java-based Configuration:
```
@Configuration
public class MyConfig {
    @Autowired
    private MyDependency myDependency;

    @Bean
    public MyBean myBean() {
        return new MyBean();
    }

    @Bean
    public MyDependency myDependency() {
        return new MyDependency();
    }
}
```
- *Autowiring by constructor*: In this mode, wiring is done using the constructor of the autowired bean by looking for a bean whose type is compatible with the constructor argument. \
XML Configuration:
```
<bean id="myBean" class="com.example.MyBean" autowire="constructor"/>
<bean id="myDependency" class="com.example.MyDependency"/>
```
Java-based Configuration:
```
@Configuration
public class MyConfig {
    @Autowired
    private MyDependency myDependency;

    @Bean
    public MyBean myBean() {
        return new MyBean(myDependency);
    }

    @Bean
    public MyDependency myDependency() {
        return new MyDependency();
    }
}
```

### 30.What are some of the important Spring Core Annotations?
Some of the spring core framework annotations are: 
- *@Configuration*: Used to indicate that a class declares one or more @Bean methods. These classes are processed by the Spring container to generate bean definitions and service requests for those beans at runtime.
- *@Bean*: Indicates that a method produces a bean to be managed by the Spring container. This is one of the most used and important spring annotation. @Bean annotation also can be used with parameters like name, initMethod and destroyMethod.
1. name – allows you give name for bean
2. initMethod – allows you to choose method which will be invoked on context register
3. destroyMethod – allows you to choose method which will be invoked on context shutdown \
For example:
```
@Configuration
public class AppConfig {

    @Bean(name = "comp", initMethod = "turnOn", destroyMethod = "turnOff")
    Computer computer(){
        return new Computer();
    }
}
```
```
public class Computer {

    public void turnOn(){
        System.out.println("Load operating system");
    }
    public void turnOff(){
        System.out.println("Close all programs");
    }
}
```
- *@PreDestroy* and *@PostConstruct* are alternative way for bean initMethod and destroyMethod. It can be used when the bean class is defined by us. For example;
```
 public class Computer {

    @PostConstruct
    public void turnOn(){
        System.out.println("Load operating system");
    }

    @PreDestroy
    public void turnOff(){
        System.out.println("Close all programs");
    }
}
```
- *@ComponentScan*: Configures component scanning directives for use with @Configuration classes. Here we can specify the base packages to scan for spring components.
- *@Component*: Indicates that an annotated class is a “component”. Such classes are considered as candidates for auto-detection when using annotation-based configuration and classpath scanning.
- *@PropertySource*: provides a simple declarative mechanism for adding a property source to Spring’s Environment. There is a similar annotation for adding an array of property source files i.e @PropertySources.
- *@Service*: Indicates that an annotated class is a “Service”. This annotation serves as a specialization of @Component, allowing for implementation classes to be autodetected through classpath scanning.
- *@Repository*: Indicates that an annotated class is a “Repository”. This annotation serves as a specialization of @Component and advisable to use with DAO classes.
- *@Autowired*: Spring @Autowired annotation is used for automatic injection of beans. Spring @Qualifier annotation is used in conjunction with Autowired to avoid confusion when we have two of more bean configured for same type.

### 31.How do you solve NoUniqueBeanDefinitionException?
> public class NoUniqueBeanDefinitionException extends NoSuchBeanDefinitionException
- Exception thrown when a BeanFactory is asked for a bean instance for which multiple matching candidates have been found when only one matching bean was expected.
- There are two simple ways you can resolve the *NoUniqueBeanDefinitionException* exception in Spring. You can use the *@Primary* annotation, which will tell Spring when all other things are equal to select the primary bean over other instances of that type for the autowire requirement.
- The second way, is to use the *@Qualifier* annotation. Through the use of this annotation, you can give Spring hints about the name of the bean you want to use. By default, the reference name of the bean is typically the lower case class name.
  
### 32.How do you solve NoSuchBeanDefinitionException?
> public class NoSuchBeanDefinitionException extends BeansException
- Exception thrown when a BeanFactory is asked for a bean instance for which it cannot find a definition. This may point to a non-existing bean, a non-unique bean, or a manually registered singleton instance without an associated bean definition. \
Reasons to cause NoSuchBeanDefinitionException and their solution :
1. *The bean doesn't exist, it wasn't registered*
- There are multiple ways to register bean definitions(Refer que.7)
2. *Expected single matching bean, but found 2 (or more)*
- Refer que.6
3. *Using wrong bean name*
- Check for bean name as exception suggests

### 33.What is @Primary?
- *@Primary* annotation in Spring is used to indicate the primary bean when multiple beans of the same type are present for auto wiring. When multiple beans are eligible for auto wiring the @Primary annotation will help to determine which bean should be given preference. 
- By applying @Primary annotation to a specific bean we are specifying that it is a primary bean for its respective type. When auto-wiring the dependencies if we are having multiple beans then the bean which is annotated with @Primary annotation will be given high preference compared to other beans.
   
For more info refer <a href="https://www.geeksforgeeks.org/spring-primary-annotation/" target="_blank">gfg</a>

### 34.What is @Qualifier?
- There may be a situation when you create more than one bean of the same type and want to wire only one of them with a property. In such cases, you can use the *@Qualifier* annotation along with @Autowired to remove the confusion by specifying which exact bean will be wired.

For more info refer <a href="https://www.baeldung.com/spring-qualifier-annotation" target="_blank">baeldung</a>

### 35.What is CDI (Contexts and Dependency Injection)?
- CDI stands for "context and dependency injection", while Spring is a complete ecosystem around a dependency injection container.
- Dependency injection is handled by both containers. The main difference is the fact that CDI handles DI in a dynamic (aka: stateful) way - this means that dependencies are resolved at execution time.
- Spring's approach is static - this means that components are wired together at creation time. While the CDI-way might seem a bit unusual at a first glimpse, it's far superior and offers way more and advanced options (I'm writing this with the background of two productive CDI apps).
  
### 36.What are the major features in different versions of Spring?
- Spring 2.0 provided XML namespaces and AspectJ support.
- Spring 2.5 made annotation-driven configuration possible.
- Spring 3.0 made great use of the Java 5 improvements in language.
- Spring 4.0 is the first version to fully support Java 8 features. Minimum version of Java to use Spring 4 is Java SE 6.
  
### 37.What are new features in Spring Framework 4.0?
1. spring-websocket module provides support for WebSocket-based communication in web applications.
2. Spring Framework 4.0 is focused on Servlet 3.0+ environments
3. @RestController annotation is introduced for use with Spring MVC applications
4. Spring 4.1 introduces @JmsListener annotations to easily register JMS listener endpoints.
5. Spring 4.1 supports JCache (JSR-107) annotations using Spring’s existing cache configuration.
6. Jackson’s@JsonViewissupporteddirectlyon@ResponseBodyandResponseEntitycontroller methods for serializing different amounts of detail for the same POJO

### 38.What are new features in Spring Framework 5.0?
1. Baseline Upgrades \
To build and run Spring 5 application, you will need a minimum JDK 8 and Java EE 7.
Similar to Java baseline, there are changes in baselines of many other frameworks as well. e.g. Hibernate 5,Jackson 2.6,JUnit 5
2. JDK 9 Compatibility
3. JDK 8 Features are Baked In \
Spring 5 has baseline version 8, so it uses many new features of Java 8 and 9 as well. e.g.Java 8 default methods,Use of functional programming in the framework code – lambdas and streams.
4. Support for Reactive Programming
5. A Functional Web Framework
6. Kotlin Support

### 39.What is the simplest way of ensuring that we are using single version of all Spring related dependencies?
- Spring is made up of a number of small components (spring-core, spring-context, spring-aop, spring-beans and so on). One of the quirks of using Spring framework is the dependency management of these components. Simple way of doing this is using Maven "Bill Of Materials" Dependency.
```
<dependencyManagement>
    <dependencies>
        <dependency> 
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>4.1.6.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```
All spring dependencies can now be included in this and the child poms without using version.
```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId> 
    </dependency>
    <dependency> 
        <groupId>org.springframework</groupId> 
        <artifactId>spring-web</artifactId>
    </dependency>
<dependencies>
```

### 40.Name some of the design patterns used in Spring Framework?
1. Singleton pattern
2. Factory Method pattern
3. Proxy pattern
4. Template pattern
