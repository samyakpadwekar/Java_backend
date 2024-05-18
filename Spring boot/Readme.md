### Interview questions for Spring boot,Spring Data (JPA and REST)

### Q. What is Spring Boot?
- Spring Boot is an open-source framework designed to simplify the setup, configuration, and development of production-ready Spring applications.
- It takes away much of the boilerplate code and configuration required in traditional Spring applications, allowing developers to focus on writing business logic.

### Q. What are the important Goals of Spring Boot?
The key goals of Spring Boot are:
- To provide a quick and efficient way to create standalone, production-ready Spring applications.
- To eliminate the need for extensive configuration by using sensible defaults.
- To enable a microservices-based architecture with built-in support for embedded servers and cloud integration.

### Q. What are the important Features of Spring Boot?
Some essential features of Spring Boot include:
1. *Auto Configuration*: Automatically configures common components based on project dependencies. ex. @EnableAutoConfiguration or @SpringBootApplication annotated class.
2. *Starter Projects*: Pre-configured templates for various types of applications.(starter dependencies)
3. *Embedded Servers*: Support for embedding web servers like Tomcat or Jetty.
4. *Spring Boot Actuator*: Built-in tools for monitoring and managing applications.
5. *Spring Initializr*: A web-based tool for generating Spring Boot projects.
6. *Externalized Configuration*: Easy management of application properties.

### Q. Compare Spring Boot vs Spring?
1. Spring is an open-source lightweight framework widely used to develop enterprise applications.
- Spring Boot is built on top of the conventional spring framework, widely used to develop REST APIs.
2. The most important feature of the Spring Framework is dependency injection.
- The most important feature of the Spring Boot is Autoconfiguration.
3. To run the Spring application, we need to set the server explicitly.
- Spring Boot provides embedded servers such as Tomcat and Jetty etc.
4. To run the Spring application, a deployment descriptor is required.
- There is no requirement for a deployment descriptor.
5. It doesn’t provide support for the in-memory database.
- It provides support for the in-memory database such as H2.
6. Developers need to write boilerplate code for smaller tasks.
- In Spring Boot, there is reduction in boilerplate code.

### Q. Compare Spring Boot vs Spring MVC?
- *Spring MVC* is a complete HTTP oriented MVC framework managed by the Spring Framework and based in Servlets. It would be equivalent to JSF in the JavaEE stack. The most popular elements in it are classes annotated with @Controller, where you implement methods that can be accessed using different HTTP requests. It has an equivalent @RestController to implement REST-based APIs.
- *Spring boot* is a utility for setting up applications quickly, offering an out of the box configuration in order to build Spring-powered applications. As you may know, Spring integrates a wide range of different modules under its umbrella, as spring-core, spring-data, spring-web (which includes Spring MVC, by the way) and so on. With this tool you can tell Spring how many of them to use and you'll get a fast setup for them (you are allowed to change it by yourself later on).
- So, Spring MVC is a framework to be used in web applications and Spring Boot is a Spring based production-ready project initializer. 

### Q. What is @SpringBootApplication,it's significance and what will happen if we don't use it?
- Many Spring Boot developers like their apps to use auto-configuration, component scan and be able to define extra configuration on their "application class". A single **@SpringBootApplication** annotation can be used to enable those three features, that is:
- *@EnableAutoConfiguration*: enable Spring Boot’s auto-configuration mechanism.
- *@ComponentScan*: enable @Component scan on the package where the application is located.
- *@Configuration*: allow to register extra beans in the context or import additional configuration classes.

### Q.Explain @Component, @Service, @Repository, @Configuration, @EnableAutoConfiguration, @ComponentScan, @EntityScan, @Transient, @Bean.
1. *@Component* :
- generic stereotype annotation for any spring-managed component.
- indicates that a class is a Spring component and it can be auto-detected during classpath scanning.
- tyically used for creating beans without any specific stereotype (e.g.@Service,@Repository) or to mark a custom class as a Spring bean.
2. *@Service* :
- specialization of @Component and is typically used to annotate service classes.
- these classes hold the business logic and are often used in the service layers of an application.
- automatically discovered and registered as Spring beans
3. *@Repository* :
- another specialization of @Compoent and is typically used to annotate repository (data access) classes.
- used to indicate that the class provides the mechanism for storage, retrieval, update, delete and search operation on objects.
- often work with databases and Spring's Data Access/Integration technologies.
4. *@Configuration* :
- The @Configuration annotation is a Spring framework annotation that indicates that a class defines one or more Spring beans or configuration methods.
- It is used to define configuration classes that provide bean definitions or configuration for the Spring container.
5. *@EnableAutoConfiguration* :
- The @EnableAutoConfiguration annotation is a Spring Boot-specific annotation that enables Spring Boot's auto-configuration feature.
- It automatically configures various components and settings based on the project's dependencies, reducing manual configuration efforts.
- Spring Boot's auto-configuration simplifies the setup of a Spring Boot application by providing sensible defaults. Without it, you would need to configure many components manually.
6. *@EntityScan* :
- When writing our Spring application we will usually have entity classes – those annotated with @Entity annotation. We can consider two approaches to placing our entity classes:
a. Under the application main package or its sub-packages.
b. Use a completely different root package .
- In the first scenario, we could use @EnableAutoConfiguration to enable Spring to auto-configure the application context.
- In the second scenario, we would provide our application with the information where these packages could be found. For this purpose, we would use @EntityScan.
- @EntityScan annotation is used when entity classes are not placed in the main application package or its sub-packages. In this situation, we would declare the package or list of packages in the main configuration class within @EntityScan annotation.
- This will tell Spring where to find entities used in our application.
- We should be aware that using @EntityScan will disable Spring Boot auto-configuration scanning for entities.
7. *@ComponentScan* :
- Similar to @EntityScan and entities, if we want Spring to use only a specific set of bean classes, we would use @ComponentScan annotation.
- It’ll point to the specific location of bean classes we would want Spring to initialize.
- This annotation could be used with or without parameters. Without parameters, Spring will scan the current package and its sub-packages, while, when parameterized, it’ll tell Spring where exactly to search for packages.
- Concerning parameters, we can provide a list of packages to be scanned (using basePackages parameter) or we can name specific classes where packages they belong to will also be scanned (using basePackageClasses parameter).

### Q. What is Auto Configuration?
- Auto Configuration is a fundamental feature of Spring Boot. 
- It is a mechanism that automatically configures various components and settings within your Spring Boot application based on the libraries and dependencies you have in your project. 
- The primary goal of auto configuration is to reduce the need for manual configuration, making it easier to set up and run Spring Boot applications.
- Auto Configuration is automatically enabled in Spring Boot applications by default. There's typically no need to enable it explicitly; it's an integral part of the Spring Boot framework.
- For example, if you include the spring-boot-starter-data-jpa dependency, Spring Boot will configure a data source and entity manager.

### Q. What is an embedded server? Why is it important?
- An embedded server, such as Tomcat or Jetty, is a web server that is bundled within the application.
- Spring Boot's embedded servers simplify deployment because you don't need to separately install and configure a server.
- It's especially important for creating self-contained, executable JAR files.

### Q. What is the default embedded server with Spring Boot? What is the default port of tomcat in spring boot?
- The default embedded server with Spring Boot is Tomcat. It's included by default when you use Spring Boot for web applications.
- The default port of the tomcat server-id 8080. It can be changed by adding *sever.port* properties in the application.property file.

### Q. What are the other embedded servers supported by Spring Boot?
- Spring Boot supports several embedded servers, including Jetty, Undertow, and more. You can choose a different server by adding the corresponding dependency to your project.

### Q. What are Starter Projects?Give examples of few important starter projects.
- Starter Projects are pre-configured templates that provide a baseline setup for different types of applications. They include specific dependencies and configurations to kickstart your development.
1. spring-boot-starter-web: For building web applications.
2. spring-boot-starter-data-jpa: For data access with JPA.
3. spring-boot-starter-security: For adding security features.
4. spring-boot-starter-test: For testing with JUnit and other testing frameworks.

### Q. What is POM Parent?
- In Spring Boot, the "Parent POM" (Project Object Model) is a special kind of POM file that contains common configuration settings and dependencies for multiple related projects.
- It serves as a template for your project's POM file, allowing you to inherit and reuse common configurations without duplicating them in each individual project.
- The Spring Boot Parent POM is specifically designed for Spring Boot applications and includes default configurations, dependency management, and plugin settings that are commonly used in Spring Boot projects.

### 15. What are the different things that are defined in Starter Parent?
- Starter Parent defines the Spring Boot version, plugin configurations, and common dependencies. It ensures that all Starter projects have compatible versions and configurations.

### 16. What is Depenednecy management?How does Spring Boot enforce common dependency management for all its Starter projects?
- Spring Boot dependency management is used to manage dependencies and configuration automatically without you specifying the version for any of that dependencies.
- Spring Boot enforces common dependency management by specifying a version for all dependencies in the Parent POM. This ensures that all Starter projects use the same versions of Spring Boot and related libraries.

### 17. What is Spring Initializer?
- Spring Initializer is a user-friendly web-based tool that helps developers create the initial structure and setup for Spring Boot applications without having to do it manually.
- It simplifies the process of setting up a Spring Boot project by generating a basic project structure with all the necessary dependencies and configuration files.
- [*Visit the Spring Initializer Website*](https://start.spring.io/)

### Q. What is application.properties?
- application.properties is a configuration file commonly used in Spring Boot applications to manage application-specific settings and properties.
- It plays a crucial role in configuring various aspects of your Spring Boot application without modifying the source code.
- You can customize properties related to database configuration, logging levels, server settings, external service URLs, and any other configuration needed for your application.
- This file is especially useful for externalizing configuration(another way is application.yml) from your codebase, making it easier to modify settings without recompiling the application.Spring Boot will automatically load these properties when the application starts.

### Q.Why is application.properties Required?
- *External Configuration*: It allows you to configure your application externally. Instead of hardcoding configuration values within your code, you can specify them in the application.properties file. This makes it easier to change settings without modifying your code, which is crucial for configuring applications across different environments (e.g., development, testing, production).
- *Maintainability*: Separating configuration from code improves the maintainability of your application. You can change configuration values without needing to recompile the application, making it more flexible and adaptable.
- *Profile Management*: Spring Boot supports profiles, which enable you to define different configurations for different environments (e.g., application-dev.properties for development and application-prod.properties for production). By using application.properties along with profiles, you can manage configuration settings for various scenarios efficiently.

### Q.What is Application.yaml?
- application.yaml (or application.yml) is an alternative configuration file format used in Spring Boot applications, alternative to the the more common application.properties file.
- Both formats serve the same purpose: configuring your Spring Boot application.
- However, they have different syntax and features, allowing you to choose the one that suits your preferences and needs.

### Q. How can you add custom application properties using Spring Boot?
- We can use @PropertySource to load a custom properties file.
```
@Component
@PropertySource("classpath:server.properties")
public class ServerProperties {

    @Value("${server.name}")
    private String name; // Value = 'SpringAppCluster01'
}
```
- Multiple property files
```
@PropertySource({
    "classpath:/server/db.properties",
    "classpath:/server/file.properties"
})
```
@PropertySources example.
```
@PropertySources({
      @PropertySource("classpath:/server/db.properties"),
      @PropertySource("classpath:/server/file.properties")
})
```

### Q. What is a Profile and why is it used?
- A profile in Spring Boot allows you to define different sets of configurations for different environments or scenarios. It helps manage application behavior in various contexts (e.g., development, production).
- While developing the application we deal with multiple environments such as dev, QA, Prod, and each environment requires a different configuration.
- For eg., we might be using an embedded H2 database for dev but for prod, we might have proprietary Oracle or DB2. Even if DBMS is the same across the environment, the URLs will be different.
- To make this easy and clean, Spring has the provision of Profiles to keep the separate configuration of environments.

### Q. How do you define beans for a specific profile?
- In Spring Boot, you can define beans for specific profiles by using the @Profile annotation.
- This annotation allows you to conditionally create or configure beans based on the active profiles in your application..
- For example:
```
@Bean
@Profile("dev")
public DataSource devDataSource() {
    // Configuration for the development profile
}
```

### Q. How do you create application configuration for a specific profile?
- You can create separate configuration files for different profiles by naming them as application-{profile}.properties or application-{profile}.yml. Spring Boot will load the appropriate configuration based on the active profile.
- For the dev profile, create a file named application-dev.properties or application-dev.yml (if you prefer YAML configuration).
- For the prod profile, create a file named application-prod.properties or application-prod.yml.
- These files should be located in the same directory as your application.properties or application.yml file.

### Q. What is Spring Boot Actuator?
- Spring Boot Actuator is a set of production-ready features and tools provided by Spring Boot for monitoring and managing your application in a production environment.
- It's like having a dashboard for your Spring Boot application that gives you insights into how your application is performing, its health, and various runtime metrics.

### Q.Why Spring boot actuator is required?
1. *Monitoring and Management*: Spring Boot Actuator helps you monitor the health, performance, and behavior of your application in real-time. You can check if your application is running properly, detect issues, and manage its components without interrupting service.
2. *Debugging and Troubleshooting*: It provides essential information about the application's internals, such as environment properties, memory usage, and configuration. This information is invaluable for debugging and troubleshooting issues in production.
3. *Security*: Spring Boot Actuator offers security measures to restrict access to sensitive endpoints, ensuring that only authorized personnel can access and manage your application's internals.
4. *Operational Insights*: It collects and exposes metrics and statistics about your application, which can help operations teams gain insights into resource usage, bottlenecks, and overall system health.
5. *Integration with Monitoring Tools*: Spring Boot Actuator seamlessly integrates with popular monitoring and management tools like Prometheus, Grafana, and Spring Cloud Sleuth, making it easier to manage your application in a larger ecosystem.

### Q.How to implement Spring boot actuator?
- using Spring Boot Actuator is as simple as adding a dependency to your project and enabling it with a few configurations. Here's an example:
1. *Add the Spring Boot Actuator dependency to your pom.xml (if you're using Maven) or build.gradle (if you're using Gradle)*:
```
<!-- Maven -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
2. *Configure Spring Boot Actuator in your application.properties or application.yml file*:
```
management.endpoints.web.exposure.include=*
```
This configuration allows all management endpoints to be exposed over the web.

### Q. How do you monitor web services using Spring Boot Actuator?
- You can use Actuator's built-in endpoints to monitor web services. For example, the /actuator/health endpoint provides information about the application's health, /actuator/metrics offers various metrics and /actuator/env displays environment properties, including application properties and system properties..
 
### Q.How to enable debugging log in the spring boot application?
- Debugging logs can be enabled in three ways -
1. We can start the application with --debug switch.
2. We can set the logging.level.root=debug property in application.property file.
3. We can set the logging level of the root logger to debug in the supplied logging configuration file.

### 3Q. What is a CommandLineRunner?
- A CommandLineRunner is an interface in Spring Boot that allows you to execute code when the application starts. It's often used for tasks like database initialization or data loading.
- Here's a simple example of a CommandLineRunner:
```
@Component
public class MyCommandLineRunner implements CommandLineRunner {

    @Override
    public void run(String... args) throws Exception {
        // Your startup code here
    }
}
```

### Q. What is a EnableTransactionManagement and Transactional annotation?
- The *@EnableTransactionManagement* annotation and *@Transactional* annotation work together to manage transactions in a Spring application, but they serve different purposes:
- **@EnableTransactionManagement**: This annotation is used at the configuration level (typically on a @Configuration class) to enable Spring's annotation-driven transaction management capability within the application. It activates Spring's ability to interpret @Transactional annotations and manage transactions accordingly. This is used to have more control over Transaction management as it allows you to specify the TransactionManager to be used for transactional methods, while @Transactional uses the default transaction manager.
- **@Transactional**: This annotation is applied at the method level or on a class, indicating that the methods (or all methods within the annotated class) should be wrapped in a transaction. It defines the scope of a single database transaction. This annotation provides metadata that Spring uses to create a transactional proxy around the annotated method or class to manage transactional behavior.
- The @Transactional annotation will work without @EnableTransactionManagement as long as you have spring-tx and a transactional resource (e.g. DataSource) in your application. Spring will detect the @Transactional annotation and configure a PlatformTransactionManager (e.g. JpaTransactionManager) for you.

### Q.Explain what isolation & propagation parameters are for in the @Transactional annotation via real-world example?
- **Propagation**
Defines how transactions relate to each other. Common options:
- *REQUIRED*: Code will always run in a transaction. Creates a new transaction or reuses one if available.
- *REQUIRES_NEW*: Code will always run in a new transaction. Suspends the current transaction if one exists.
The default value for @Transactional is REQUIRED, and this is often what you want.

- **Isolation**
Defines the data contract between transactions.
- *ISOLATION_READ_UNCOMMITTED*: Allows dirty reads.
- *ISOLATION_READ_COMMITTED*: Does not allow dirty reads.
- *ISOLATION_REPEATABLE_READ*: If a row is read twice in the same transaction, the result will always be the same.
- *ISOLATION_SERIALIZABLE*: Performs all transactions in a sequence.
  
- The different levels have different performance characteristics in a multi-threaded application. I think if you understand the dirty reads concept you will be able to select a good option.

### JPA and Spring Data JPA

### Q. Can you explain the difference between JPA and JDBC?
- JDBC is a standard for Database Access
- JPA is a standard for ORM
- JDBC is a standard for connecting to a DB directly and running SQL against it - e.g SELECT * FROM USERS, etc. Data sets can be returned which you can handle in your app, and you can do all the usual things like INSERT, DELETE, run stored procedures, etc. It is one of the underlying technologies behind most Java database access (including JPA providers).
- One of the issues with traditional JDBC apps is that you can often have some crappy code where lots of mapping between data sets and objects occur, logic is mixed in with SQL, etc.
- JPA is a standard for Object Relational Mapping. This is a technology which allows you to map between objects in code and database tables. This can "hide" the SQL from the developer so that all they deal with are Java classes, and the provider allows you to save them and load them magically. Mostly, XML mapping files or annotations on getters and setters can be used to tell the JPA provider which fields on your object map to which fields in the DB. The most famous JPA provider is Hibernate, so it's a good place to start for concrete examples.

### Q. What is the difference between JPA and Hibernate?
1. JPA is a specification. In fact, it is a set of interfaces, and vendors provide actual implementations.
2. Hibernate from RedHat is the most popular implementation.
3. There exist other JPA implementations, e.g., EclipseLink or Apache OpenJPA.
4. Each of them must comply with the JPA specification.
5. Apart from this, some of them usually provide vendor-specific APIs not described in the spec.

### Q.Name the main JPA objects
In the JPA specification, there are the following main objects:
1. *Entity*
– a class that is mapped to a database table. Its fields correspond to the columns of the table.

2. *MappedSuperclass*
– a class that declares common attributes for entities. We use this class to build an entity hierarchy to reuse common attributes.
- Each table associated with an entity from the hierarchy in the database will contain all fields from the MappedSuperclass entity and its descendants.

3. *Embeddable*
– a class that we can embed into other entities.
- If we need to treat a pack of fields as one entity and reuse it in various entities, then an embeddable class is what we need.
- use @Embeddable/@Embedded when you have a value object that is tightly coupled to its parent entity. Use regular entity mapping when you have independent objects with their own identity.

4. *EntityManager*
– a facility that allows us to manage the lifecycle of the JPA entity instance.
- EntityManager API is a part of the JPA specification.
- We can create, read, update or delete an entity from a database by using it.
- EntityManager allows us to execute SQL queries to select entities.
- Also, we can use a special query language - JPQL – to fetch data.
*JPQL is similar to SQL but uses classes and attributes in queries instead of tables and columns*.

5. *Session*
– the Hibernate-specific interface that extends the EntityManager.
- All methods defined by the EntityManager are available in the Hibernate Session.
- Many other methods in it are unique to Hibernate, e.g., isDirty(), evict(), cancelQuery() and so on...
  
- Then, you may have a reasonable question: "In which cases is it better to use EntityManager, and in which cases is Session"?
- I will quote Emmanuel Bernard, a data architect on the JBoss Hibernate team. He gives the following answer:
"We encourage people to use the EntityManager. From a team point of view, we wish we had only one API. We are trying to push into the standard as much as we can.
If we could somehow merge or deprecate the Session in the future, we would do it, but people still use some stuff that is not in the EntityManager, and we don't want to just break everybody's application just for the fun of it."
- So, try to use EntityManager whenever it's possible, and when you have no choice but to use Session, unwrap it from the EntityManager:

### Q. Which association types and mappings could you specify?
- Like in the relational database model, there are four association types in JPA: one-to-one, one-to-many, many-to-one, and many-to-many.
- You can define all of them as uni- or bi-directional.
- It means you can create an attribute in only one of the associated entities or both.
1. *Uni-directional many-to-one association* "One User can create Many Posts":
```
@Entity 
public class User { 

    //id, first name, last name, etc. 
    //No references to the Post entity. The association is unidirectional. 

} 

@Entity 
public class Post { 

    //... 
    @ManyToOne(fetch = FetchType.LAZY) 
    @JoinColumn(name = "user_id") 
    private User user; //reference to the User entity 
    //... 

}
```
2. *Bi-directional one-to-many/many-to-one association* "One User can create Many Posts":
```
@Entity 
public class User { 
    //... 
    @OneToMany (mappedBy = "user") 
    private Set<Post> posts = new HashSet<>(); //reference to collection of posts created by the User 
    //... 
} 

@Entity 
public class Post { 
    //... 
    @ManyToOne 
    @JoinColumn(name = "user_id") 
    private User user; //reference to the User entity 
    //... 
}
```
- In the relational databases, we have only unidirectional relations (defined as foreign keys).
- ORM engine gives us more flexibility by providing bi-directional ones.
- For the latter, we should always keep in mind the limitations of the database side.Thus, when we define a bi-directional association, we should know which side of it is the "owning" one.
- An association's "owning" side is responsible for keeping the reference.The corresponding table will have the reference column and foreign key constraint.
- The "owning" side reference must be populated. Otherwise, the association will not be stored.
- For the example above, if we add a Post instance to the User,posts collection and save the User entity, the association won't be saved. But if we assign the Post.user field, everything will be OK.(as Poat is the owning side)

NOTE: To quickly figure out which side is the "owning" one, just look at the annotation on the reference field. \
If there is the *mappedBy* attribute – this is the inverse side of the association; otherwise – the owning one.

### Q. Entity ID, what is it?
- According to the JPA specification, Entity is a Java class that meets the following requirements:
1. Annotated with @Entity annotation;
2. Has no-args constructor;
3. Is not final;
4. Has an ID field (or fields).
- As you can see, ID is required.The reason is simple - ORM engines use the ID to identify each entity instance stored in the database uniquely.
- In 99% of cases, IDs are generated. To avoid issues with uniqueness, it is important to choose the right way to generate an ID.
- We can use a client- or database-generation ID strategy. Which, in its turn, are divided into several more sub-strategies.
- When choosing ID type and generation strategy, the rule of thumb is: for the single DB instance, and monolithic application, the server-side ID generation using sequence is the best choice in most cases.
- If we have microservice architecture and distributed databases, it is better to use UUIDs generated on the client.
- In some cases, we can use composite IDs consisting of several attributes.
- One of these attributes is often a reference to another entity.
- Composite keys are common, especially when we build an application over the existing database.

### Q. What does the hbm2ddl.auto/ddl-auto property stand for?
- In fact, it is a single property, but it has two names. The first one – hibernate.hbm2ddl.auto is used by "pure" Hibernate, while the second one – spring.jpa.hibernate.ddl-auto is a Spring wrapper over the first one.
- This property instructs ORM on what to do with the database schema.
- There are five possible values for it:
1. create – first, Hibernate will drop the database tables mapped to the entities. Then, it will generate and execute a DDL to create a DB schema that complies with the JPA model.
2. create-drop – will do the same as the previous one, but Hibernate will drop the database tables mapped to the entities after the application shuts down.
3. update – Hibernate will generate DDL scripts only for new tables/columns in this mode. Even though the value is called update, it does not create scripts to change or drop existing columns.
4. validate – in this mode, Hibernate will not generate any DDL statements and won't touch your database. It will only check for full compliance of your JPA model with the database.
5. none – will do nothing.
- Indeed, all you need to know about the ddl-auto property is that it's not a good idea to use any of the above values except validate on the production stand.
- For testing, create/create-drop may be an OK choice.
- And if you don't want to re-fill the database every time while testing, you can use the update option.
- For better development experience, prefer specialized solutions to manage database changes like Liquibase or Flyway. Even simple .sql files written by hand or automatically generated by the JPA Buddy in conjunction with spring.sql.init.mode would do better because you:
1. have complete control over the DDL before its execution;
2. can set up proper Java to Database types mapping;
3. have no issues using the attribute converters and Hibernate types.

### Q. Ways to fetch data from the database using JPA?
a. *JPQL*
b. *Criteria API*
c. *QueryDSL*
d.*Spring Data JPA @Query/Derived methods*
e. *Native Queries*

### 8. What are the states of an entity in JPA?
JPA specifies four different object states:
1. *Transient* – All new entities have never been associated with an opened database session (Persistence Context) and do not have corresponding rows in the database yet;
2. *Managed* – All entities fetched from the database and associated with a Persistence Context. ORM tracks all the changes made to entities in this state. When we close the session without transaction rollback, ORM automatically submits all changes to the database;
3. *Detached* – Entities transit to this state when the database session is closed. The ORM no longer tracks any changes made to them. To save entities, we need to make them managed again by "attaching" them to the session. The simplest way is to invoke EntityManager's merge() method. Some frameworks (like Spring Data JPA) can do it automatically.
4. *Removed* – entities get into this state after we call the remove() method. They will only be removed from the database after we flush session changes or close it.

### Q. What does @Transactional annotation do? What are the ways to configure it?
- A database transaction is a sequence of actions treated as a single unit of work.
- In other words, either all actions will be executed or none.
- Spring provides a powerful mechanism for managing transactions.
- Simply annotating a method with @Transactional, we automatically open a database transaction when the method execution starts and close the transaction when it finishes.
- 


## 11. Have you ever stumbled upon the LazyInitException? If so, how did you get rid of it?
- The LazyInitializationException is probably one of the most common exceptions in the JPA world.
- Hibernate throws it when you refer to the association that was not loaded from the database, and the entity is detached. Here is a simple example:
```
entityManager.getTransaction().begin();   

TypedQuery<User> query = entityManager.createQuery(  
    "SELECT u FROM User u",  
    User.class);  
List<User> users = query.getResultList();  

entityManager.getTransaction().commit();  
entityManager.close();  

for (User user : users) {  
    int size = user.getProfiles().size(); //Here we are stumbling upon LazyInitializationException. 
}
``` 
- Hibernate cannot load the required field from the database when an entity is detached. If we look at the error message, we'll see something like this.
``` 
Exception in thread "main" org.hibernate.LazyInitializationException: failed to lazily initialize a collection of role: entities.User.profiles: could not initialize proxy - no Session ...  
```
- For lazy loaded attribute values, Hibernate creates proxy classes that use the existing session to load actual values at the first read attempt.
- Therefore, if the session is closed, the loading fails.
- You might think that the most straight-to-the-point way to fix it – execute all the code inside the transaction context.
- In fact, it is. But in this case, you'll get rid of LazyInitException but get an N+1 problem.
- So, the right way to fix it - fetch all the required data in one query using a join clause.
- For example:
```
entityManager.getTransaction().begin();

TypedQuery<User> query = entityManager.createQuery(  
    "SELECT u FROM User u join fetch u.profiles",  
    User.class);  
List<User> users = query.getResultList();  

entityManager.getTransaction().commit();  
entityManager.close();  

for (User user : users) {  
    int size = user.getProfiles().size();  
    log.info(String.format("User with id=%d has %d profiles", user.getId(), size));  
}  
```

### 12. Apart from JPQL, what are the other ways to select associated entities from the database? (EntityGraph, DTO, Projection)
- To avoid the N+1 problem and LazyInitException, we can use the join statement in the JPQL. 
- But there are other options to specify the attributes and associations we want to select. They are:
1. Entity graph – specified in JPA standard;
2. DTOs and projections – used by Spring Data JPA library.
- Let's have a look at them in detail.
1. *Entity Graph*
- The entity graph feature has been introduced in JPA 2.1.
- It has been one of the most awaited features for a long time.
- Entity Graphs give us another layer of control over data that needs to be fetched.
- In Spring Data JPA, we can specify the required data right above the @Query declaration.
- The example below shows how to fetch the User entity along with its profiles attribute:
```
@EntityGraph(attributePaths = {"profiles"}) 
List<User> findUserByEmailAndName(String email, String firstName);
``` 
Also, we can specify a named entity graph for an entity and reuse it in different places. For example, we can use the graph with the entity manager:
```
@NamedEntityGraph (name = "user-with-profiles", 
  attributeNodes = {@NamedAttributeNode("profiles")} 
) 
@Entity 
public class User { 
    //... 
} 
//... 

EntityGraph entityGraph = entityManager.getEntityGraph("user-with-profiles"); 
Map<String, Object> properties = new HashMap<>(); 
properties.put("javax.persistence.fetchgraph", entityGraph); 
Post post = entityManager.find(User.class, id, properties);
```
- In Spring Data JPA, it will look like this:
```
@EntityGraph(value = "user-with-profiles") 
List<User> findUserByEmailAndName(String email, String firstName);
``` 
2. *DTO and Projection*
- DTO (data transfer object) is an object that carries data between processes.
- DTOs for JPA entities generally contain a subset of entity attributes.
- Spring Data JPA allows us to specify DTOs as a method return type in repositories.
- Under the hood, Spring Data optimizes the query to fetch only attributes defined in the DTO.
- We can specify DTO as a class:
```
public class UserDto implements Serializable { 
    private final String firstName; 
    private final String email; 

    public UserDto(String firstName, String email) { 
        this.firstName = firstName; 
        this.email = email; 
    } 

    //getters and setters are omitted   
}
``` 
… or as an interface. 
- Spring Data JPA derives attribute names from the interface's method names.
- So, for the following definition, it is assumed that the entity has attributes firstName and lastName.
```
public interface UserDto { 
    String getFirstName();  
    String getLastName(); 
}
```
The use of DTO does not differ in any way from the repository methods:
```
List<UserDto> findUserByEmailAndName(String email, String firstName); 
```
As a result, we improve queries efficiency because only specific fields are retrieved from the database. For the repository definition above, the query will be:
```
    select u1_0.first_name, u1_0.last_name from "user" u1_0
```

### 13. What is Lombok library? How is it useful for JPA, and how can it harm?
- Lombok is a library targeted to replacing boilerplate code writing with annotations and bytecode instrumentation.
- For example, we don't need to write getters and setters, all we need to do is to annotate class with @Getter and @Setter and these methods will be generated automatically in runtime.
- It looks like an ideal library to clean up JPA entities code, but to use lombok right, we need to deeply understand which exactly methods are generated and what is inside.
- Classic example: generated equals() and hashCode() methods may cause LazyInitException. By default, they use all fields, including associations.
- Associations in their turn, may be lazily initialized.
- When we add detached entities into a collection, the collection class invokes the equals() method under the hood... so, we get the exception.
- For attached entities, we get an extra query that loads associated entities. Anyway, it is definitely what we expect from the method invocation.
- To avoid it, we should explicitly exclude associations from those methods by annotating correspondent fileds by @ToString.Exclude.

### 14. What is better for *-to-many associations: List<> or Set<>?
- In JPA, efficiency is not about data structures being used for entities, but about queries.
- Both List and Set can cause N+1 problem, that can be resolved by using JPQL, entity graph, or projections in Spring Data JPA.
- In contrast to List, Set cannot contain duplicate elements.
- It means that we need to define equals() and hashCode() methods for the child entity, which is good practice anyway.
- List is more common in JPA world, but we need to remember one thing.
- Let's have a look at the following entity and related repository which selects an owner with all their pets:
```
@Entity 
public class Owner { 
    //id, name 
    @OneToMany(mappedBy = "owner", cascade = CascadeType.ALL, orphanRemoval = true) 
    private List<Dog> dogs = new ArrayList<>(); 

    @OneToMany(mappedBy = "owner", cascade = CascadeType.ALL, orphanRemoval = true) 
    private List<Cat> cats = new ArrayList<>(); 

    //setters, getters 
} 

public interface OwnerRepository extends JpaRepository<Owner, Long> { 
    @EntityGraph(attributePaths = {"dogs", "cats"}) 
    List<Owner> findByNameLikeIgnoreCase(String name); 
} 
```
- If we use two one-to-many associations with List collection and try to fetch both eagerly, we will get MultipleBagFetchException on the application start.
- The reason why Hibernate throws this exception is that duplicates can occur with two associations.
- The List is implemented by the PersistentBag in Hibernate and the latter cannot deal with duplicates.
- In this case, replacing Lists to Sets can help, but there is a big drawback – we will get cartesian product in the query.
- It can greatly impact the query performance. We'll get the following SQL
```
    select 
        ...  
    from 
        owner owner0_  
    left outer join 
        dog dogs1_  
            on owner0_.id=dogs1_.owner_id  
    left outer join 
        cat cats2_  
            on owner0_.id=cats2_.owner_id  
    where 
        upper(owner0_.name) like upper(?) escape ?
```
- To fix this for good, we need to split data fetching into two queries and fetch the owner two times with two collections separately in one transaction as recommended in this article.
- The L1 cache will help us to merge the second collection into the existing Owner entities.
```
public interface OwnerRepository extends JpaRepository<Owner, Long> { 
    @EntityGraph(attributePaths = {"cats"}) 
    List<Owner> findWithCatsByNameLikeIgnoreCase(String name); 
  
    @EntityGraph(attributePaths = {"dogs"}) 
    List<Owner> findWithDogsByNameLikeIgnoreCase(String name); 
 
    @Transactional 
    default List<Owner> findByNameLikeIgnoreCase (String name) { 
        List<Owner> ownersWithCats = findWithCatsByNameLikeIgnoreCase(name); 
        List<Owner> ownersWithDogs = findWithDogsByNameLikeIgnoreCase(name); 
        return ownersWithDogs; //or cats, they are the same in L1 cache 
    } 

} 
```

#### 1.What is Spring Data REST?
- Spring Data REST is a part of the Spring Data project that simplifies the creation of RESTful web services for your data repositories.
- It allows you to expose your Spring Data repositories as RESTful endpoints with minimal configuration, reducing the amount of code required to create a fully functional REST API.
- Spring Data REST is built on top of Spring Data JPA, Spring Data MongoDB, Spring Data Cassandra, and other Spring Data modules.

#### 2.Why We Need Spring Data REST?
1 .*Rapid API Development*: Spring Data REST allows you to create a RESTful API quickly, often with minimal custom code. It automates many common tasks such as CRUD operations, query methods, and pagination. \
2. *Consistency and Best Practices*: Spring Data REST enforces best practices for building RESTful APIs, ensuring that your API follows standard conventions and is consistent in its design. \
3. *Reduced Boilerplate Code*: You can avoid writing repetitive code for common REST API features like URL mapping, request/response handling, and pagination. \
4. *Flexibility and Customization*: While Spring Data REST provides automatic endpoints, you can customize and extend these endpoints as needed to add business logic or control the API's behavior. \

-----
let's walk through an example of implementing Spring Data JPA and then enhancing it with Spring Data REST. We'll use a simplified "Book" entity and repository for this demonstration. \

*Step 1: Implement Spring Data JPA* \
First, let's set up Spring Data JPA to manage our "Book" entity. We'll create an entity class, a repository interface, and a service class to handle business logic. \
*Book Entity*:
```
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String author;

    // Constructors, getters, setters, etc.
}
```
*Book Repository*: 
```
public interface BookRepository extends JpaRepository<Book, Long> {
    // Spring Data JPA provides CRUD methods
    List<Book> findByAuthor(String author);
}
```
*Book Service (optional, for business logic)*: \
```
@Service
public class BookService {
    @Autowired
    private BookRepository bookRepository;

    // Business logic methods
}
```
Now, we have a basic Spring Data JPA setup where you can create, read, update, and delete books using repository methods. \

*Step 2: Enhance with Spring Data REST* \
Now, let's enhance our application by adding Spring Data REST to expose our "Book" repository as a RESTful API with minimal code changes. \

*BookRepository Configuration*: \
```
@RepositoryRestResource(collectionResourceRel = "books", path = "books")
public interface BookRepository extends JpaRepository<Book, Long> {
    List<Book> findByAuthor(String author);
}
```
We added the @RepositoryRestResource annotation to our repository interface. This annotation customizes the REST endpoint for books by specifying the collectionResourceRel (plural name of the resource) and the path (endpoint path). This tells Spring Data REST how to expose the repository as a REST API. \

*Main Application Class*: \
```
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
With these minimal changes, you have enhanced your Spring Data JPA application with Spring Data REST. Pagination and sorting are also supported out of the box. \
Spring Data REST also supports more advanced features like custom queries, projections, validation, and event handling. These can be configured and extended based on your application's specific needs.

In summary, Spring Data REST simplifies the process of creating RESTful APIs for your data repositories by providing automatic CRUD endpoints, adhering to RESTful conventions, and reducing the amount of boilerplate code required for API development. It's a powerful tool for quickly exposing your data to the web.

-----

### 3.How do you enable Spring Data REST in a Spring Boot application?
- To enable Spring Data REST in a Spring Boot application, you typically need to include the spring-boot-starter-data-rest dependency in your project's pom.xml (for Maven) or build.gradle (for Gradle).
```
<!-- For Maven -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-rest</artifactId>
</dependency>
```

### 4.What is a Repository in Spring Data REST?
- A Repository in Spring Data REST is an interface that extends CrudRepository or PagingAndSortingRepository and is automatically exposed as a RESTful resource.
- It provides CRUD operations for an entity.
```
// Example of a repository interface
public interface UserRepository extends CrudRepository<User, Long> {
}
```

### 5.How do you expose a repository as a RESTful resource in Spring Data REST?
- Spring Data REST automatically exposes repositories as RESTful resources.
- You only need to include the repository interface in your project, and it becomes accessible via HTTP.

### Q.What is Sorting and Pagination in spring boot,how to do it?


### Q.How can you restrict the HTTP methods allowed on a Spring Data REST endpoint, also how can this endpoints customised?
- assume we want to hide the delete method from third parties while being able to use it internally.Then, we can use the annotation @RestResource(exported = false), which will configure Spring to skip this method when triggering the HTTP method exposure:

```
@Override
@RestResource(exported = false)
void deleteById(Long aLong);
```
- The @RestResource annotation also gives us the ability to customize the URL path mapped to a repository method and the link id in the JSON returned by the HATEOAS resource discovery. To do that, we use the optional parameters of the annotation:
- **path for the URL path**
- **rel for the link id**

- If we don’t like the default path, instead of changing the repository method, we can simply add the @RestResource annotation:
```
@RestResource(path = "byEmail", rel = "customFindMethod")
WebsiteUser findByEmail(@Param("email") String email);
```

### Q.What is the purpose of event handlers in Spring Data REST, and how can you define them?
- Event handlers in Spring Data REST allow you to intercept and customize repository events (e.g., before save, after delete). You can define them by creating a bean that implements ApplicationListener.
```
@Component
public class MyEventHandler implements ApplicationListener<BeforeSaveEvent> {
    @Override
    public void onApplicationEvent(BeforeSaveEvent event) {
        // Custom logic before save
    }
}
```

### Q.How do you secure Spring Data REST endpoints?
- use various security mechanisms to achieve this, such as Spring Security (OAuth2,jwt), to ensure that only authenticated and authorized users can perform operations on your RESTful API.

### Q.What is a custom search method in Spring Data REST, and how do you define one?
- A custom search method in Spring Data REST allows you to define your own search criteria and expose it as an HTTP endpoint in your RESTful API.
- This is useful when you need to perform complex searches on your data that go beyond simple CRUD operations.
- Custom search methods give you the flexibility to query your data based on specific requirements.
  
```
public interface UserRepository extends CrudRepository<User, Long> {
    List<User> findByLastName(String lastName);
}
```

### Q.What is Spring boot Rest Controller?how is it beneficial?
- The @RestController annotation in Spring is used to declare a class as a RESTful controller.
- It tells Spring that this class will handle incoming HTTP requests and send HTTP responses, typically in JSON or XML format. In simple terms, it makes your Java class act like a web service.
```
@RestController
public class MyRestController {
    // Your controller methods here
}
```
1. *Simplified Development*: @RestController simplifies the development of RESTful web services in Spring. It combines @Controller and @ResponseBody annotations, making it easier to create web services that directly return data, typically in JSON or XML, without needing to annotate each method with @ResponseBody.
2. *Automatic Serialization*: It automatically serializes the response data into JSON or XML format. This means you can return regular Java objects from your methods, and Spring takes care of converting them into the appropriate format for the HTTP response.


### Q.What HTTP methods are commonly used in RESTful web services, and how does Spring boot support them?
- Common HTTP methods are GET, POST, PUT, DELETE, etc. Spring supports these methods by directly using HTTP specific annotation (@GetMapping, @PostMapping, @PutMapping, @DeleteMapping) or through the @RequestMapping annotation, by specifying the method in the annotation, you can control which HTTP method should trigger your method.
```
@RequestMapping(value = "/create", method = RequestMethod.POST)
public ResponseEntity<String> createResource() {
    // Create a resource here
}

---

@GetMapping("/students") 
public List<Student> getAllStudents() { 
return studentRepository.findAll(); 
} 

```

### Q.How do you handle request and response serialization in Spring REST?
- Spring automatically handles request and response serialization using libraries like *Jackson*.
- When you return an object from your controller method, Spring converts it to JSON or XML (based on content negotiation) for the response. When a JSON or XML request is received, Spring deserializes it into a Java object.

### Q.What is JSON Binding?
- JSON data binding is the process of converting JSON data (JavaScript Object Notation) to Java objects and vice versa.
- It allows you to seamlessly work with JSON data in your Java applications by providing mechanisms to serialize (convert Java objects to JSON) and deserialize (convert JSON to Java objects) data.
- In Spring Boot, JSON data binding is implemented using the Jackson library, which is a popular and widely used library for JSON processing in Java.
- Jackson provides a set of classes and annotations that allow you to map Java objects to JSON data and back.

For detailed explanation refer <a href="https://www.geeksforgeeks.org/how-jackson-data-binding-works-in-spring-boot/" target="_blank">gfg article</a>

**API versioning**

### Q.Explain the concept of versioning in RESTful APIs, and how can it be implemented in Spring?
- Versioning in RESTful APIs is a practice of providing multiple versions of your API to clients.
- It allows you to make changes to your API while ensuring that existing clients can continue to use the older versions without disruption.
- Versioning is essential to maintain compatibility and manage the evolution of your API over time.
- Here are a few common methods of implementing versioning in RESTful APIs:
1. *URI Versioning*: URL path versioning involves including the version number directly in the URL path of the API endpoints. This is a common approach and makes the version explicit in the URL.
 ```
@RestController
@RequestMapping("/v1/users")
public class UserControllerV1 {
    // Endpoint implementations...
}
``` 
2. *Request Header Versioning*: In this approach, the API version is specified in a custom HTTP request header. 
```
@RestController
@RequestMapping("/users")
public class UserController {
    
    @GetMapping(headers = "API-Version=1")
    public ResponseEntity<String> getUserV1() {
        // Endpoint implementation for version 1
    }
    
    @GetMapping(headers = "API-Version=2")
    public ResponseEntity<String> getUserV2() {
        // Endpoint implementation for version 2
    }
}
```

3. *Request Parameter Versioning*: In this approach, the version number is included as a query parameter in the URL.
```
@RestController
@RequestMapping("/users")
public class UserController {
    
    @GetMapping(params = "version=1")
    public ResponseEntity<String> getUserV1() {
        // Endpoint implementation for version 1
    }
    
    @GetMapping(params = "version=2")
    public ResponseEntity<String> getUserV2() {
        // Endpoint implementation for version 2
    }
}
```
4. *Media Type (Accept Header) Versioning*: In this approach, the version is specified in the Accept header of the HTTP request.
```
@RestController
@RequestMapping("/users")
public class UserController {
    
    @GetMapping(produces = "application/vnd.company.app-v1+json")
    public ResponseEntity<String> getUserV1() {
        // Endpoint implementation for version 1
    }
    
    @GetMapping(produces = "application/vnd.company.app-v2+json")
    public ResponseEntity<String> getUserV2() {
        // Endpoint implementation for version 2
    }
}
```
For detailed explanation refer <a href="https://medium.com/@avi.singh.iit01/a-guide-to-api-versioning-in-spring-boot-d564595bba00" target="_blank"> medium article</a>


**Exception handling**

### Q.How can you handle exceptions in a Spring REST application?
To handle exceptions in a Spring Boot application, you can use the following strategies:
- *Global Exception Handling*: Implement a global exception handler using @ControllerAdvice and @ExceptionHandler to catch and handle exceptions at the application level.
- *Controller-Level Exception Handling*: Use @ExceptionHandler at the controller level to handle exceptions specific to a controller.
- *Service-Level Exception Handling*: Catch and handle exceptions within service classes using try-catch blocks.
- *Custom Exception Classes*: Create custom exception classes to provide more detailed error information.
- *Logging and Monitoring* : Use logging and monitoring tools to track and analyze exceptions for debugging and improvement. \
By implementing these strategies, you can effectively handle exceptions in a Spring Boot application, providing a better user experience and improving application reliability.

For detailed explanation refer <a href="https://naveen-metta.medium.com/mastering-exception-handling-in-spring-boot-a-comprehensive-guide-fa3f916d1981#:~:text=In%20Spring%20Boot%2C%20you%20have,exceptions%2C%20managing%20specific%20HTTP%20status" target="_blank"> medium article</a>

**Caching**

### Q.Explain the concept of caching in Spring boot and how it can improve performance.
- Caching in Spring Boot is a mechanism that stores frequently accessed data in memory to reduce the number of database queries and improve application performance.
- It acts as a bridge between the server and the end-user, delivering data on-demand in real-time.
- By caching data, applications can avoid redundant database calls, reducing latency and improving scalability.

### Q.How Cache is implemented in Spring boot?
- Spring provides caching support through its caching abstraction, which allows you to easily enable caching for specific methods in your application. Here's how to do it:
1. *Enable Caching*: To use caching in a Spring application, you need to enable it in your configuration. In a Spring Boot application, this is often done by simply adding the @EnableCaching annotation to your main application class.
```
@SpringBootApplication
@EnableCaching
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
2. *Annotate Methods*: To cache the results of specific methods, you can use annotations like @Cacheable, @CachePut from the Spring Framework. These annotations allow you to control when and how caching is applied.
```
@Service
public class MyService {
    @Cacheable("users")
    public User getUserById(Long userId) {
        // This method's result will be cached with the "users" cache name
        return userRepository.findById(userId);
    }
}
```
In this example, the getUserById method retrieves a user by ID from a database, and the result is cached with the name "users."
3. *Configure Cache Providers*: By default, Spring uses an in-memory cache provider (e.g., Caffeine or EhCache) that comes with Spring Boot. However, you can configure other cache providers like Redis or Memcached for distributed caching.
4. *Cache Eviction*: The @CacheEvict annotation is used to trigger cache eviction, which removes entries from the cache.
Specify the cache names from which you want to remove entries and set allEntries = true to remove all entries from the specified caches.
```
@CacheEvict(cacheNames = {"users", "address"}, allEntries = true)
public void evictCache() {
    LOG.info("Evict all cache entries...");
}
```
- In the provided example, the evictCache() method is annotated with @CacheEvict to remove all entries from the caches named "users" and "address".
- When this method is invoked, all entries in the specified caches will be removed, ensuring that stale or unnecessary data is cleared from the cache.

- *Accessing cached data*
- To access the cached data, you can invoke the method that is annotated with @Cacheable. When this method is called with the same arguments, Spring will check the cache for the result before executing the method.
- If the result is found in the cache, it will be returned directly without executing the method again, improving performance by avoiding redundant computations.
- In the provided example, the getUserById method is annotated with @Cacheable("users"). When this method is called with a specific id, Spring will check the cache named "users" for the result associated with that id.
- If the result is cached, it will be returned from the cache. If not, the method will be executed, and the result will be stored in the cache for future access.


### Rest API

### Q.Why use RESTful web service?
1. Minimizes coupling between client and server
2. Ideal for multiple, independent clients
3. Supports frequent server updates without affecting clients
4. Uses standard HTTP protocols for easy client development
5. Stateless connections simplify load balancing and service partitioning
6. Adheres to HTTP rules, enabling effective use of tools like debuggers and caching proxies
7. Provides a robust, scalable, and flexible architecture for distributed applications

### Q.What are some best practices for designing and implementing RESTful APIs in Spring boot? or REST Api best practice?
1. *Use descriptive and meaningful resource names*:
- Instead of generic or ambiguous names, choose resource names that accurately represent the entities they represent. (e.g., /api/customers/123 instead of /api/users/123).
2. *Use HTTP methods correctly*:
- Use the appropriate HTTP methods (GET, POST, PUT, DELETE, PATCH, etc.) for different operations.
3. *Version Your API*:
- Use versioning to ensure backward compatibility and allow for future enhancements without breaking existing clients.
- Consider using URI versioning (e.g., /api/v1/resource) or request header versioning (e.g., Accept: application/vnd.myapp.v1+json).
4. *Use HTTP Status Codes Correctly*:
-Use appropriate HTTP status codes to indicate the result of an API request (e.g., 200 for success, 201 for resource creation, 400 for client errors, 500 for server errors).
5. *Pick your JSON field naming convention (and stick to it)*:
- JSON standard doesn’t impose a field naming convention, but it’s a best practice to pick one and stick with it.(example : snake_case, camelCase, PascalCase, kekab-Case).
6. *Document Your API*:
- Provide comprehensive documentation for your APIs, including endpoint details, request/response examples, and usage guidelines.
- SWAGGER/OPENAPI DOCUMENTATION
- MARKDOWN-BASED DOCUMENTATION (E.G., USING TOOLS LIKE SWAGGER UI OR REDOC)
7. *Use consistent error messages*:
- In most cases, HTTP status codes are not enough to explain what went wrong.
- To help your API consumers, include a structured JSON error message.
- The response should include the following information-
- *Error code*: A machine-readable error code that identifies the specific error condition.
- *Error message*: A human-readable message that provides a detailed explanation of the error.
- *Error context*: Additional information related to the error, such as the request ID, the request parameters that caused the error, or the field(s) in the request that caused the error.
- *Error links*: URLs to resources or documentation that provide additional information about the error and how it can be resolved.
- *Timestamp*: The time when the error occurred.
8. *Use query parameters for filtering, sorting, and searching*:
- Query parameters allow you to provide additional information in the URL of an HTTP request to control the response returned by the server.
- Filter : Returns only relevant result for specific request. Example : /users?name={name}
- Sort : Order result in specific manner. Example : /users?sort_by=age
- Paginate : Divide results into mangeable parts or pages. Example : /users?page={page_number}&per_page={results_per_page}
9. *Implement authentication and authorization*:
- Secure your APIs by implementing proper authentication and authorization mechanisms.
- USE API KEYS, TOKENS, OR OAUTH 2.0 FOR AUTHENTICATION
- APPLY ROLE-BASED ACCESS CONTROL (RBAC) FOR AUTHORIZATION
10. *Do not maintain state*:
- A REST API should not maintain a state on the server. That’s the responsibility of the client.
- This is important because it allows for the API to be cacheable, scalable, and decoupled from the client.
- For example, an e-commerce API might use cookies to maintain the state of a shopping cart. However, such an approach violates the key principle of RESTful APIs — they need to be stateless.


**Annotations**

1. *@RestController*:@RestController is a specialized version of the controller. It includes the @Controller and @ResponseBody annotations, and as a result, simplifies the controller implementation.Every request handling method of the controller class automatically serializes return objects into HttpResponse.
2. *@Controller*:This annotation is used to mark a class as a web request handler. It's typically used in combination with annotated handler methods based on the @RequestMapping annotation.
3. *@ResponseBody*:You can use the @ResponseBody annotation on a method to have the return serialized to the response body through an HttpMessageWriter. @ResponseBody is also supported at the class level, in which case it is inherited by all controller methods.
4. *@RequestBody*:It is used to bind the HTTP request body to the parameter in the controller method.Used with POST, PUT, and PATCH requests where data is sent in the request body.
5. *@RequestMapping*:The @RequestMapping annotation is used to map requests to controllers methods. It has various attributes to match by URL, HTTP method, request parameters, headers, and media types. You can use it at the class level to express shared mappings or at the method level to narrow down to a specific endpoint mapping.
6. *@GetMapping, @PostMapping, @PutMapping, @DeleteMapping*:These annotations are used to map HTTP requests to specific methods in a controller class. They're variations of @RequestMapping with specific HTTP methods.
7. *@RequestParam*:extract values from the query string. ex. http://localhost:8080/spring-mvc-basics/foos?id=abc -> ID: abc (@GetMapping("/foos"))
8. *@PathVariable*:extract values from the URI. ex. http://localhost:8080/spring-mvc-basics/foos/abc -> ID: abc (@GetMapping("/foos/{id}"))


### @.What is the role of the @RequestBody and @ResponseBody annotations?
- The @RequestBody and @ResponseBody annotations are used to handle data in the request and response of a web service, making it easier to work with data in your Spring applications. Let's break down their roles with simple code examples:
1. *@RequestBody Annotation*:
- @RequestBody is applicable for the incoming request data, used with POST, PUT, PATCH methods to read the request body, return type is typically void or a simple type, deserialized object is passed as a method parameter, required to read JSON/XML request payloads.
2. *@ResponseBody Annotation*:
- @ResponseBody is typically for the outgoing response data, the object returned is automatically serialized into JSON ,used with GET methods to write the response body content, return type is typically a complex object representing the response data, serialized object is returned from the method, required to write JSON/XML response payloads.
```
public class EmployeeController { 
    @Autowired
    private EmployeeRepository employeeRepository; 
  
    @ResponseBody
    @PostMapping
    public Employee 
    addPerson(@RequestBody Employee employee) 
    { 
        return employeeRepository.save(employee); 
    } 
  
    @ResponseBody
    @GetMapping
    public List<Employee> getAllEmployee() 
    { 
        return employeeRepository.findAll(); 
    } 
  
    @ResponseBody
    @GetMapping("/{id}") 
    public Employee getEmployeeById(@PathVariable Long id) 
    { 
        return employeeRepository.findById(id).orElse(null); 
    } 
}
```

### Q.What is the purpose of the @PathVariable annotation in, hos is it different from @RequestParam?
- @RequestParam and @PathVariable can both be used to extract values from the request URI, but they are a bit different. Here's an explanation of each with code examples and their differences:

1. *@PathVariable*:
- Purpose: The @PathVariable annotation is used to extract values from the URI path. It can be made optional by using the required attribute starting with Spring 4.3.3. We should be careful when making @PathVariable optional, to avoid conflicts in paths.
```
http://localhost:8080/spring-mvc-basics/foos/abc
----
ID: abc

@GetMapping("/foos/{id}")
@ResponseBody
public String getFooById(@PathVariable(required = false) String id) {
    return "ID: " + id;
}
```

2. *@RequestParam*:
- @RequestParams extract values from the query string. Query parameters are the key-value pairs added to the URL after a **?** symbol. For @RequestParam, we can also use the required attribute.
```
http://localhost:8080/spring-mvc-basics/foos?id=abc
----
ID: abc

@GetMapping("/foos")
@ResponseBody
public String getFooByIdUsingQueryParam(@RequestParam String id) {
    return "ID: " + id;
}
```

### Q.Explain the purpose of the @RequestMapping,@PostMapping,@PutMapping,@GetMapping,@DeletMapping annotation in Spring REST.
- @RequestMapping is a general-purpose annotation for mapping any HTTP method, whereas @PostMapping, @PutMapping, and @GetMapping are specialized annotations for mapping POST, PUT, and GET requests, respectively.
- The specialized annotations make the code more expressive and easier to understand because they clearly indicate the intended HTTP method.
- Using specialized annotations helps in code readability and can also help prevent mistakes where the wrong HTTP method is inadvertently used.
```
@RequestMapping(value = "/resource", method = RequestMethod.GET)
public ResponseEntity<String> getResource() {
    // Handle GET request for /resource
}
```

2. *@PostMapping*:
- The POST method is used to create a new resource on the server. For example, if you want to create a new user, you can use a POST request to /users with the user data in the request body. In Spring Boot, you can use the @PostMapping annotation to map a method to a POST request.
```
@PostMapping("/users")
  public User createUser(@RequestBody User user) {
    return userService.createUser(user);
  }
```

3. *@PutMapping*:
- The PUT method is used to update a resource on the server. For example, if you want to update an existing user, you can use a PUT request to /users/{id} with the updated user data in the request body. In Spring Boot, you can use the @PutMapping annotation to map a method to a PUT request
```
@PutMapping("/users/{id}")
  public User updateUser(@PathVariable Long id, @RequestBody User user) {
    return userService.updateUser(id, user);
  }
```

4. *@GetMapping*:
- TThe GET method is used to retrieve a resource from the server. For example, if you want to get a list of users, you can use a GET request to /users. In Spring Boot, you can use the @GetMapping annotation to map a method to a GET request.
```
@GetMapping("/users")
  public List<User> getAllUsers() {
    return userService.getAllUsers();
  }
```

5. *@DeleteMapping*
- The DELETE method is used to delete a resource from the server. For example, if you want to delete an existing user, you can use a DELETE request to /users/{id}. In Spring Boot, you can use the @DeleteMapping annotation to map a method to a DELETE request.
```
@DeleteMapping("/users/{id}")
  public void deleteUser(@PathVariable Long id) {
    userService.deleteUser(id);
  }
```
6. *@PatchMapping*
- The PATCH method is used to partially update a resource on the server. For example, if you want to update only some fields of an existing user, you can use a PATCH request to /users/{id} with the modified user data in the request body. In Spring Boot, you can use the @PatchMapping annotation to map a method to a PATCH request.
```
@PatchMapping("/users/{id}")
  public User patchUser(@PathVariable Long id, @RequestBody User user) {
    return userService.patchUser(id, user);
  }
```

### Q.Difference between @Controller and @RestController?
- Spring 4.0 introduced the @RestController annotation in order to simplify the creation of RESTful web services. It’s a convenient annotation that combines @Controller and @ResponseBody, which eliminates the need to annotate every request handling method of the controller class with the @ResponseBody annotation.
1. @Controller -
- a specialization of the @Component class, which allows us to auto-detect implementation classes through the classpath scanning.
- common annotation used to create Spring MVC controllers that are responsible for processing web requests.
- typically used in traditional web appls where the response is usually a web page (HTML view).
- these controllers generally return views(HTML pages) that are rendered by a templating engine (e.g.,Thymeleaf,JSP) and sent to the client's web browser.
- We typically use @Controller in combination with a @RequestMapping annotation for request handling methods.

2. @RestController -
- @RestController is a specialized version of the controller.
- It is a combination of behaviours of a Controller and ResponseBody.
- When we use this Annotation, the response is JSON or XML. Because of this, the Controller is not in charge of providing any viewpoint to the user.
- Every request handling method of the controller class automatically serializes return objects into HttpResponse.

### Q.How does @Compoent and @Service annotation works internally?what difference will it make if we use @Component instead of @Service or vice versa?
- Internally when Spring scans the components in application context,it identifies classed annotated with @Component, @Service, @Repository etc. and registers them as beans in the Spring IOC container.
- These beans can then be injected into other components,and their lifecycle is managed by the container.

 *Differences* :
 1. Expressiveness and Semantic Clarity : @Service provides a more expressive and semantic meaning to a class, indicating that it is a service component.This can improve code readability and make the purpose of the class more apparent.
 2. Component Scannig : Both annotations trigger component scanning, and, from a functionality standpoint, there is no difference between using @Component and @Service.The difference lies in the intended use and the clarity of the code.
 3. Consideration for the layered architecture : @Service is often used in the service layer of a typical layered architecture (like MVC),making it a good fit for services with business logic.@Component is more generic and can be used for any component.

- Both annotation work similarly and using one over the other doesn't affect the core functionality of the Spring.The choice between both annoation depends on your preference for semantic clarity and the intended use of annotated class in your application architecture.
- They are interchangeable from a functional standpoint,and use of one above other is matter of convention and redability.

### Q.Why use @Valid and @RequestBody annotation?
- **@Valid**
1. Ensures that incoming request data is validated against specified constraints.
2. Improves data integrity by automatically checking for validation errors.
3. Simplifies error handling by leveraging built-in validation mechanisms.

- **@RequestBody**
1. Maps the body of an HTTP request to a Java object.
2. Simplifies data binding by automatically deserializing JSON/XML into the application's model.
3. Facilitates the handling of incoming data in a structured and consistent manner.


### Questions as per dependency added in project

### Q.Why is Jackson dependency used in Spring boot?important jackson dependencies?
- Jackson is one of the most used libraries of spring boot which translates JSON data to a Java POJO by itself and vice-versa. JSON stands for JavaScript-object-Notation and POJO is our plain-old-java-object class. 
- important jackson dependencies :
1. *jackson-databind* : General data-binding functionality for Jackson: works on core streaming API.
2. *jackson-core*: Core Jackson processing abstractions (aka Streaming API), implementation for JSON.
3. *jackson-annotations*: This library includes annotations like @JsonProperty, @JsonFormat, and others that you can use to customize the JSON mapping behavior.

