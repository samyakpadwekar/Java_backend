# Spring-Core-Interview-Question

### what is spring framework?
### what are the features of spring?
### what are the modules of spring?
### What is Loose Coupling?
### What is a Dependency?
### What Is a Spring Bean?
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

### How to create a Spring bean?
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
### How to Define the Scope of a Bean?
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
### What Is the Default Bean Scope in Spring Framework?
- Singleton scope is the default scope in Spring Framework.

### What are the other scopes available?
There are five scopes defined for Spring Beans.
- *singleton* - Only one instance of the bean will be created for each container. This is the default scope for the spring beans. While using this scope, make sure bean doesn’t have shared instance variables otherwise it might lead to data inconsistency issues.
- *prototype* - A new instance will be created every time the bean is requested.
- *request* - This is same as prototype scope, however it’s meant to be used for web applications. A new instance of the bean will be created for each HTTP request.
- *session* - A new bean will be created for each HTTP session by the container.
- *global-session* - This is used to create global session beans for Portlet applications.
Spring Framework is extendable and we can create our own scopes too. However, most of the times we are good with the scopes provided by the framework.

### How is Spring’s singleton bean different from Gang of Four Singleton Pattern?
- GOF Singleton Pattern as per Wikipedia
> A Java singleton, per the design pattern where instantiation is restricted to one, usually per class loader by the code.
- Spring Singleton as per Spring 3.1 Doc
> A Spring singleton bean can be any normal class you write, but declaring it's scope as singleton means that Spring will only create one instance and provide its reference to all beans that reference the declared bean. You may have many instances of that class in your application, but only one will be created for that bean. You may even have multiple beans of the same class all declared as singleton. Each bean will create exactly one instance of the class.
- The *Java singleton Pattern* is scoped by the Java class loader, the *Spring singleton* is scoped by the container context.
Which basically means that, \
- In Java, you can be sure that a singleton is a truly a singleton only within the context of the class loader which loaded it. Other class loaders should be capable of creating another instance of it (provided the class loaders are not in the same class loader hierarchy), despite of all your efforts in code to try to prevent it.
- In Spring, if you could load your singleton class in two different contexts and then again we can break the singleton concept.
- So, in summary, Java considers something a singleton if it cannot create more than one instance of that class within a given class loader, whereas Spring would consider something a singleton if it cannot create more than one instance of a class within a given container context.
- Even if we declare same bean two different times, it will be created just once. Spring is smart enough to handle that and when you try to fetch instances via IDs, can be tested using "==" operator.

### Are Singleton Beans Thread-Safe?
### What Does the Spring Bean Lifecycle Look Like?
### What are Bean Factory and Application Context?
### Can you compare Bean Factory with Application Context?
### How do you create an application context with Spring?
### What are the different options available to create Application Contexts for Spring?
### How does Spring know where to search for Components or Beans?
### What is the difference between XML and Java Configurations for Spring?
### How do you choose between XML and Java Configurations for Spring?
### How do you define a component scan in XML and Java Configurations?
### What is IOC (Inversion of Control)?
### What is Dependency Injection?
### Can you give few examples of Dependency Injection?
### What are the important roles of an IOC Container?
### How Can We Inject Beans in Spring?
### What is setter injection?
### What is constructor injection?
### Which Is the Best Way of Injecting Beans and Why?
### What is Auto Wiring?
### How does Spring do Autowiring?
### What are the different modes of Autowiring in Spring?
### How is it done with Spring Boot?
### What does @Component signify?
### What is a Component Scan?
### What does @Autowired signify?
### What’s the difference Between @Controller, @Component, @Repository, and @Service Annotations in Spring?
### How do you debug problems with Spring Framework?
### How do you solve NoUniqueBeanDefinitionException?
### How do you solve NoSuchBeanDefinitionException?
### What is @Primary?
### What is @Qualifier?
### What is CDI (Contexts and Dependency Injection)?
### Does Spring Support CDI?
### Would you recommed to use CDI or Spring Annotations?
### What are the major features in different versions of Spring?
### What are new features in Spring Framework 4.0?
### What are new features in Spring Framework 5.0?
### What are important Spring Projects?
### What is the simplest way of ensuring that we are using single version of all Spring related dependencies?
### Name some of the design patterns used in Spring Framework?
### What do you think about Spring Framework?
### Why is Spring Popular?
### Can you give a big picture of the Spring Framework?
