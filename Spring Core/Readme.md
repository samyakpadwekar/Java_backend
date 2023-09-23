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
** Example to understand topic easily ** 
- Assume we have a class declaration:

```
public class Company {
    private Address address;

    public Company(Address address) {
        this.address = address;
    }

    // getter, setter and other properties
}
```

- This class needs a collaborator of type Address:

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
- Traditional Approach -

Normally, we create objects with their classes’ constructors:
```
Address address = new Address("High Street", 1000);
Company company = new Company(address);
```
- There’s nothing wrong with this approach, but wouldn’t it be nice to manage the dependencies in a better way? \
Imagine an application with dozens or even hundreds of classes. \
Sometimes we want to share a single instance of a class across the whole application, other times we need a separate object for each use case, and so on. \
Managing such a number of objects is nothing short of a nightmare.This is where inversion of control comes to the rescue. \
Instead of constructing dependencies by itself, an object can retrieve its dependencies from an IoC container. \
All we need to do is to provide the container with appropriate configuration metadata.

- Bean Configuration
First off, let’s decorate the Company class with the @Component annotation:
```
@Component
public class Company {
    // this body is the same as before
}
```

- Here’s a configuration class supplying bean metadata to an IoC container:

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
- The configuration class produces a bean of type Address. It also carries the @ComponentScan annotation, which instructs the container to look for beans in the package containing the Company class.
- When a Spring IoC container constructs objects of those types, all the objects are called Spring beans, as they are managed by the IoC container.

- IoC in Action -
- Since we defined beans in a configuration class, we’ll need an instance of the AnnotationConfigApplicationContext class to build up a container:
```
ApplicationContext context = new AnnotationConfigApplicationContext(Config.class);
```
- A quick test verifies the existence and the property values of our beans:
```
Company company = context.getBean("company", Company.class);
assertEquals("High Street", company.getAddress().getStreet());
assertEquals(1000, company.getAddress().getNumber());
```
The result proves that the IoC container has created and initialized beans correctly.

### How to create a Spring bean?
-
### What Is the Default Bean Scope in Spring Framework?
### How to Define the Scope of a Bean?
### What are the other scopes available?
### How is Spring’s singleton bean different from Gang of Four Singleton Pattern?
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
