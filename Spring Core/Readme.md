# Spring-Core-Interview-Question

### 1.what is spring framework?
### 2.what are the features of spring?
### 3.what are the modules of spring?
### 4.What is Loose Coupling?
### 5.What is a Dependency?
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

### 7.How to create a Spring bean?
Spring Framework provides three ways to configure beans to be used in the application. \
*Annotation Based Configuration* - By using @Service or @Component annotations. Scope details can be provided with @Scope annotation.\
*XML Based Configuration* - By creating Spring Configuration XML file to configure the beans. If you are using Spring MVC framework, the xml based configuration can be loaded automatically by writing some boiler plate code in web.xml file. \
*Java Based Configuration* - Starting from Spring 3.0, we can configure Spring beans using java programs. Some important annotations used for java based configuration are @Configuration, @ComponentScan and @Bean.

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
- *singleton* - Only one instance of the bean will be created for each container. This is the default scope for the spring beans. While using this scope, make sure bean doesn’t have shared instance variables otherwise it might lead to data inconsistency issues.
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

### 14.What is the difference between XML and Java Configurations for Spring?
### 15.How do you choose between XML and Java Configurations for Spring?
### 16.How do you define a component scan in XML and Java Configurations?

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

AnnotationConfigApplicationContext class was introduced in Spring 3.0. It accepts classes annotated with @Configuration, @Component, and JSR-330 compliant classes. The constructor of AnnotationConfigApplicationContext accepts one or more classes. \
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

AnnotationConfigWebApplicationContext class was introduced in Spring 3.0. It is similar to AnnotationConfigApplicationContext for a web environment. It accepts classes annotated with @Configuration, @Component, and JSR-330 compliant classes. These classes can be registered via register() method or passing base packages to scan() method. This class may be used when we configure ContextLoaderListener servlet listener or a DispatcherServlet in a web.xml. From Spring 3.1, this class can be instantiated and injected to DispatcherServlet using java code by implementing WebApplicationInitializer, an alternative to web.xml.
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

Spring MVC Web-based application can be configured completely using XML or Java code. Configuring this container is similar to the AnnotationConfigWebApplicationContext container, which implies we can configure it in web.xml or using java code.
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

FileSystemXmlApplicationContext is used to load XML-based Spring Configuration files from the file system or from URL. We can get the application context using Java code. It is useful for standalone environments and test harnesses. The following code shows how to create a container and use the XML as metadata information to load the beans.

Illustration:
```
String path = "Documents/demoProject/src/main/resources/applicationcontext/student-bean-config.xml";

ApplicationContext context = new FileSystemXmlApplicationContext(path);
AccountService accountService = context.getBean("studentService", StudentService.class);
```

**Container 5: ClassPathXmlApplicationContext**

FileSystemXmlApplicationContext is used to load XML-based Spring Configuration files from the classpath. We can get the application context using Java code. It is useful for standalone environments and test harnesses. The following code shows how to create a container and use the XML as metadata information to load the beans.

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
### 22.What are the different options available to create Application Contexts for Spring?
### 23.How does Spring know where to search for Components or Beans?
### 24.What is Dependency Injection?
### 25.Can you give few examples of Dependency Injection?
### 26.How Can We Inject Beans in Spring?
### 27.What is setter injection?
### 28.What is constructor injection?
### 29.Which Is the Best Way of Injecting Beans and Why?
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

### 30.What is Auto Wiring?
### 31.How does Spring do Autowiring?
### 32.What are the different modes of Autowiring in Spring?
### 33.How is it done with Spring Boot?
### 34.What does @Component signify?
### 35.What is a Component Scan?
### 36.What does @Autowired signify?
### 37.What’s the difference Between @Controller, @Component, @Repository, and @Service Annotations in Spring?
### 38.How do you debug problems with Spring Framework?
### 39.How do you solve NoUniqueBeanDefinitionException?
### 40.How do you solve NoSuchBeanDefinitionException?
### 41.What is @Primary?
### 42.What is @Qualifier?
### 43.What is CDI (Contexts and Dependency Injection)?
### 44.Does Spring Support CDI?
### 45.Would you recommed to use CDI or Spring Annotations?
### 46.What are the major features in different versions of Spring?
### 47.What are new features in Spring Framework 4.0?
### 48.What are new features in Spring Framework 5.0?
### 49.What are important Spring Projects?
### 50.What is the simplest way of ensuring that we are using single version of all Spring related dependencies?
### 51.Name some of the design patterns used in Spring Framework?
### 52.What do you think about Spring Framework?
### 53.Why is Spring Popular?
### 54.Can you give a big picture of the Spring Framework?
