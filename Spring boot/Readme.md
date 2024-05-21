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

### Q. What are the different things that are defined in Starter Parent?
- Starter Parent defines the Spring Boot version, plugin configurations, and common dependencies. It ensures that all Starter projects have compatible versions and configurations.

### Q. What is Depenednecy management?How does Spring Boot enforce common dependency management for all its Starter projects?
- Spring Boot dependency management is used to manage dependencies and configuration automatically without you specifying the version for any of that dependencies.
- Spring Boot enforces common dependency management by specifying a version for all dependencies in the Parent POM. This ensures that all Starter projects use the same versions of Spring Boot and related libraries.

### Q. What is Spring Initializer?
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

### Q. What is a CommandLineRunner?
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


### Profiling in spring boot

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

- --> For more explanation on spring boot profiling <a href="https://medium.com/javarevisited/getting-started-with-spring-boot-profiles-1e00159f0542#:~:text=Profiles%20in%20Spring%20Boot%20are,configurations%20for%20your%20production%20environment." target="_blank">medium article</a>


### Spring boot actuator

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

 - --> For video explanation on spring boot actuator <a href="https://www.youtube.com/watch?v=sATuxP_qC-4" target="_blank">utube video</a>
 - --> For documentation <a href="https://spring.io/guides/gs/actuator-service" target="_blank">spring guide</a>
 

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
- *Entity*: Represents a class that is mapped to a database table.
- *EntityManagerFactory* : Produces EntityManager instances, representing a single persistence unit.
- *EntityManager*: Interface used to interact with the persistence context, managing entity lifecycle and performing CRUD operations.
- *PersistenceContext*: Represents a set of managed entities within a persistence context. It acts as a cache for entities, tracking changes and synchronizing them with the database during transaction commits.
- *PersistenceUnit*: Defines a set of entity classes and configuration settings managed as a unit in the persistence.xml file.
- *Query*: Interface for executing JPQL or native SQL queries against the database.
- *CriteriaQuery*: Used to create type-safe queries dynamically at runtime, without writing JPQL or native SQL.
- *Transaction*: Represents a unit of work that is performed against the database. Transactions ensure data integrity by providing ACID properties (Atomicity, Consistency, Isolation, Durability).

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
- In relational databases, we typically have unidirectional relations through foreign keys.
- However, ORM engines like JPA provide bi-directional relations for more flexibility.
- When defining bi-directional associations, it's crucial to identify the "owning" side, responsible for maintaining the reference in the corresponding table.
- The owning side must populate the reference for the association to be stored properly.
- For instance, if we add a Post instance to the posts set collection and save the User entity, the association won't be saved unless we also assign the user field to Post entity(since Post is the owning side).

NOTE: To quickly figure out which side is the "owning" one, just look at the annotation on the reference field. \
If there is the *mappedBy* attribute – this is the inverse side of the association; otherwise – the owning one.

### Q. Entity ID, what is it?
- An entity ID in JPA is a unique identifier assigned to each instance of an entity class, allowing ORM engines to distinguish entities in the database.
- IDs are crucial for data management. They're often generated automatically to ensure uniqueness. Different strategies like client- or database-generation can be employed. 

### Q. What does the hbm2ddl.auto/ddl-auto property stand for?
- The hbm2ddl.auto or ddl-auto property configures how Hibernate manages the database schema.
- Five options: create, create-drop, update, validate, none.
- Use validate for production, create/create-drop for testing.

### Q. Use of each option of hbm2ddl.auto/ddl-auto property?
1. *create*: Hibernate drops existing tables, then generates and executes DDL to create a schema matching the JPA model.
2. *create-drop*: Similar to 'create', but tables are dropped when the application shuts down.
3. *update*: Generates DDL only for new tables/columns; does not modify or drop existing columns.
4. *validate*: Hibernate checks JPA model against the database for compliance without making any changes.
5. *none*: Hibernate takes no action regarding schema management.

### Q. Ways to fetch data from the database using JPA?
a. *JPQL*
b. *Criteria API*
c. *QueryDSL*
d.*Spring Data JPA @Query/Derived methods*
e. *Native Queries*

### 8. What are the states of an entity in JPA?
- JPA specifies four different object states:
- *Transient*: These are new entities that haven't been saved to the database yet and aren't tracked by the session.
- *Managed*: These entities are fetched from the database and are tracked by the session. Any changes to them are automatically saved to the database when the session ends.
- *Detached*: When the session closes, entities become detached, meaning changes to them are no longer tracked.
- *Removed*: These entities are marked for deletion after calling the remove() method. They will be deleted from the database once the session changes are saved or the session closes.

## Q. Have you ever stumbled upon the LazyInitException? If so, how did you get rid of it?
1. Access to a lazily loaded property after the session is closed
2. Accessing a lazily loaded property outside of a transaction
- In general, a LazyInitializationException means that the data of the related entity are not accessible because the main entity is no longer connected to the database, or, to put it in terms of the lifecycle stages, is Detached.
- To avoid LazyInitializationException in Hibernate, the optimal solution is to use *JPQL or HQL queries with JOIN FETCH* and *Entity Graphs* to manage the loading of related data.
- Avoid forcing eager loading, as this can lead to performance issues. Proper session and transaction management is critical for successful access to lazily loaded properties.
 
### Q. Apart from JPQL, what are the other ways to select associated entities from the database? (EntityGraph, DTO, Projection)
- To avoid the N+1 problem and LazyInitException, we can use *JPQL or HQL queries with JOIN FETCH* and *Entity Graphs*. 
1. *Entity Graph*
- Entity Graphs give us another layer of control over data that needs to be fetched.
- In Spring Data JPA, we can specify the required data right above the @Query declaration.
- The example below shows how to fetch the User entity along with its profiles attribute:
```
@EntityGraph(attributePaths = {"profiles"}) 
List<User> findUserByEmailAndName(String email, String firstName);
``` 

### Q. What is better for *-to-many associations: List<> or Set<>?
- For *-to-many associations, deciding between `List<>` and `Set<>` depends on your specific use case.
- **List<>**: Use a list when you need to maintain the order of elements or when duplicate elements are allowed. Lists are indexed, meaning you can access elements by their index. They're suitable when the order in which elements are added matters, such as preserving the order of comments on a post.
- **Set<>**: Use a set when you want to ensure uniqueness of elements and don't care about their order. Sets do not allow duplicate elements and do not maintain insertion order. They're ideal for ensuring uniqueness, such as storing unique tags associated with a post.
- In summary, use a `List<>` when you need to maintain order or allow duplicates, and use a `Set<>` when you need uniqueness and order doesn't matter.

### Spring Data REST

#### Q.What is Spring Data REST?Why we need it?
- Spring Data REST is a framework that simplifies the development of RESTful APIs by automatically exposing CRUD operations on Spring Data repositories as RESTful endpoints. It eliminates the need to write custom controllers and mappings by providing a simple way to expose CRUD operations over HTTP. It also promotes consistency and standardization in API design across projects.

### Q.How do you enable Spring Data REST in a Spring Boot application?
- To enable Spring Data REST in a Spring Boot application, you typically need to include the spring-boot-starter-data-rest dependency in your project's pom.xml (for Maven) or build.gradle (for Gradle).
```
<!-- For Maven -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-rest</artifactId>
</dependency>
```

### Q.What is a Repository in Spring Data REST?
- A Repository in Spring Data REST is an interface that extends CrudRepository or PagingAndSortingRepository and is automatically exposed as a RESTful resource.
- It provides CRUD operations for an entity.
```
// Example of a repository interface
public interface UserRepository extends CrudRepository<User, Long> {
}
```

### Q.What is Sorting and Pagination in spring boot,how to do it?
- For explanation refer <a href="https://medium.com/shoutloudz/pagination-and-sorting-using-spring-boot-103bba7bc4d7" target="_blank"> medium article</a>

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
- For more explanation <a href="https://www.geeksforgeeks.org/how-jackson-data-binding-works-in-spring-boot/" target="_blank">gfg article</a>


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
}

@RestController
@RequestMapping("/v2/users")
public class UserControllerV2 {
}
``` 
2. *Request Header Versioning*: In this approach, the API version is specified in a custom HTTP request header. 
```
    @GetMapping(headers = "API-Version=1")
    public ResponseEntity<String> getUserV1() 
    
    @GetMapping(headers = "API-Version=2")
    public ResponseEntity<String> getUserV2()
```

3. *Request Parameter Versioning*: In this approach, the version number is included as a query parameter in the URL.
```
    @GetMapping(params = "version=1")
    public ResponseEntity<String> getUserV1()

    @GetMapping(params = "version=2")
    public ResponseEntity<String> getUserV2() 
```
4. *Media Type (Accept Header) Versioning*: In this approach, the version is specified in the Accept header of the HTTP request.
```
    @GetMapping(produces = "application/vnd.company.app-v1+json")
    public ResponseEntity<String> getUserV1()
    
    @GetMapping(produces = "application/vnd.company.app-v2+json")
    public ResponseEntity<String> getUserV2() 
```
- --> For more explanation on api versioning refer <a href="https://medium.com/@avi.singh.iit01/a-guide-to-api-versioning-in-spring-boot-d564595bba00" target="_blank"> medium article</a>


**Exception handling**

### Q.How can you handle exceptions in a Spring REST application?
To handle exceptions in a Spring Boot application, you can use the following strategies:
- *Global Exception Handling*: Implement a global exception handler using @ControllerAdvice and @ExceptionHandler to catch and handle exceptions at the application level.
- *Controller-Level Exception Handling*: Use @ExceptionHandler at the controller level to handle exceptions specific to a controller.
- *Service-Level Exception Handling*: Catch and handle exceptions within service classes using try-catch blocks.
- *Custom Exception Classes*: Create custom exception classes to provide more detailed error information.
- *Logging and Monitoring* : Use logging and monitoring tools to track and analyze exceptions for debugging and improvement. \
By implementing these strategies, you can effectively handle exceptions in a Spring Boot application, providing a better user experience and improving application reliability.

**Caching**

### Q.Explain the concept of caching in Spring boot and how it can improve performance.
- Caching in Spring Boot is a mechanism that stores frequently accessed data in memory to reduce the number of database queries and improve application performance.
- It acts as a bridge between the server and the end-user, delivering data on-demand in real-time.
- By caching data, applications can avoid redundant database calls, reducing latency and improving scalability.

For detailed explanation refer <a href="https://medium.com/vedity/spring-boot-caching-mechanism-8ef901147e60" target="_blank">Spring Boot Caching Mechanism</a>


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
- *Use descriptive and meaningful resource names*: Choose resource names that accurately represent the entities they represent, like /api/customers/123 instead of /api/users/123.
- *Version Your API*: Use versioning to ensure backward compatibility and allow for future enhancements without breaking existing clients.
- *Document Your API*: Provide comprehensive documentation for your APIs, including endpoint details, request/response examples, and usage guidelines.
- *Implement authentication and authorization:* Secure your APIs by implementing proper authentication and authorization mechanisms, like using API keys or tokens and applying role-based access control (RBAC).


### Annotations

**Web Layer Annotations**
1. *@RestController*:
- Combines @Controller and @ResponseBody for simplifying controller implementations.
- Automatically serializes return objects into HttpResponse.
2. *@Controller* :
- Marks a class as a web request handler.
- Typically used with annotated handler methods (e.g., @RequestMapping).
3. *@ResponseBody* :
- Serializes return values of methods to the response body.
- Can be used at both method and class levels.
4. *@RequestBody* :
- Binds the HTTP request body to a method parameter.
- Commonly used with POST, PUT, and PATCH requests.
5. *@RequestMapping* :
- Maps web requests to specific handler methods.
- Can specify URL patterns, HTTP methods, request parameters, headers, and media types.
6. *@GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping* :
- Shortcut annotations for @RequestMapping with specific HTTP methods (GET, POST, PUT, DELETE, PATCH).
7. *@RequestParam* :
- Extracts query string parameters from the URL.
- Example: http://localhost:8080/foos?id=abc -> ID: abc (@GetMapping("/foos"))
8. *@PathVariable* :
- Extracts values from the URI path.
- Example: http://localhost:8080/foos/abc -> ID: abc (@GetMapping("/foos/{id}"))
9. *@CrossOrigin* :
- Allows cross-origin requests from specified origins.
- Can be applied to methods or classes to control CORS policy.
10. *@ExceptionHandler* :
- Defines a method to handle exceptions thrown by request handling methods.
- Can be used at the method level within a @Controller or @RestController.

**Component and Bean Annotations**
1. *@Component* :
- Generic annotation for Spring-managed components.
- Facilitates auto-detection during classpath scanning.
2. *@Service* :
- Specialized @Component for service layer classes.
- Holds business logic and is auto-registered as a Spring bean.
3. *@Repository* :
- Specialized @Component for data access classes.
- Manages storage, retrieval, and search operations for entities and is auto-registered as a Spring bean.
4. *@Configuration* :
- Indicates a class defines one or more Spring beans or configuration methods.
- Used for setting up Spring application configurations.
5. *@Bean* :
- Declares a method as a bean provider within a Spring application context.
- Allows custom initialization and dependency injection.
6. *@Primary* :
- Indicates a primary bean when multiple beans of the same type exist.
- Used to resolve ambiguity in dependency injection.
7. *@Scope* :
- Specifies the scope of a bean (e.g., singleton, prototype).
- Controls bean instantiation lifecycle.
8. *@Lazy* :
- Indicates that a bean should be lazily initialized.
- Helps improve startup performance by delaying bean creation until needed.

**Spring Boot Annotations**
1. *@EnableAutoConfiguration* :
- Enables Spring Boot's auto-configuration feature.
- Reduces manual setup by configuring components based on project dependencies.
2. *@ComponentScan* :
- Configures package locations for Spring component scanning.
- Can specify base packages for scanning Spring-managed components.
3. *@EntityScan* :
- Specifies where to find entity classes in a Spring application.
- Useful when entities are not placed in the main application package.
4. *@SpringBootApplication* :
- Combines @Configuration, @EnableAutoConfiguration, and @ComponentScan.
- Marks the main class of a Spring Boot application.
5. *@SpringBootTest* :
- Used for testing Spring Boot applications.
- Configures an application context for integration tests.

**Data Persistence Annotations**
1. *@Entity* :
- Specifies that a class is an entity and is mapped to a database table.
- Defines a persistent domain object.
2. *@Table* :
- Specifies the table in the database associated with an entity.
- Can customize table name, schema, and unique constraints.
3. *@Id* :
- Indicates the primary key of an entity.
- Used in conjunction with @GeneratedValue for automatic ID generation.
4. *@GeneratedValue* :
- Specifies the primary key generation strategy (e.g., AUTO, IDENTITY, SEQUENCE).
- Automatically generates IDs for primary key fields.
5. *@Column* :
- Specifies the mapping between a field and a column in a database table.
- Can customize column name, data type, and constraints.
6. *@JoinColumn* :
- Specifies the foreign key column for a relationship.
- Used with @ManyToOne, @OneToMany, and other relationship annotations.
7. *@OneToOne, @OneToMany, @ManyToOne, @ManyToMany* :
- Define relationships between entities.
- Specify cardinality and ownership of relationships.
8. *@Transient* :
- Indicates that a field should not be persisted to the database.
- Used for non-persistent fields in an entity class.
9. *@Embeddable* :
- Specifies a class whose instances are stored as intrinsic parts of an owning entity.
- Typically used for composite keys or value types.
10. *@Embedded* :
- Specifies that an embeddable class is to be embedded in an entity.
- Used to include non-entity classes as part of an entity.

**Validation Annotations**
1. *@Valid* :
- Ensures incoming request data is validated against specified constraints.
- Improves data integrity by automatically checking for validation errors.
2. *@NotNull, @NotEmpty, @NotBlank* :
- Ensure that a field is not null, empty, or blank.
- Used to enforce non-null constraints.
3. *@Size* :
- Specifies the size constraints for a field.
- Ensures a field's value length falls within a specified range.
4. *@Min, @Max* :
- Specify the minimum and maximum value constraints for a numeric field.
- Used for range validation.
5. *@Pattern* :
Specifies a regular expression that a field's value must match.
Used for pattern validation.
6. *@Email*:
- Ensures that a field's value is a valid email address.
- Used for email validation.
7. *@Past, @Future* :
- Ensure that a date field's value is in the past or future.
- Used for date validation.
8. *@AssertTrue, @AssertFalse* :
- Ensure that a boolean field's value is true or false.
- Used for boolean validation.

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

### Q. What is a EnableTransactionManagement and Transactional annotation?
- *@EnableTransactionManagement* enables Spring's annotation-driven transaction management capability within a Spring application. It's used at the configuration level to activate Spring's interpretation of *@Transactional* annotations and manage transactions.
- Use this annotation when you need more control over transaction management, such as specifying the TransactionManager to be used for transactional methods.
- *@Transactional* is applied at the method level or on a class to indicate that the methods (or all methods within the annotated class) should be wrapped in a transaction, defining the scope of a single database transaction.
- Apply this annotation when you want to define transactional behavior at the method level, or when you want Spring to automatically manage transactions using default configuration, such as using the default transaction manager.
- If you're using @Transactional without @EnableTransactionManagement, Spring will automatically configure a PlatformTransactionManager based on the transactional resource (e.g., DataSource) in your application.

### Q. What does @Transactional annotation do? What are the ways to configure it?
- We can use @Transactional to wrap a method in a database transaction.It allows us to set propagation, isolation, timeout, read-only, and rollback conditions for our transaction. We can also specify the transaction manager.
- We can put the annotation on definitions of interfaces, classes, or directly on methods.  They override each other according to the priority order; from lowest to highest we have: interface, superclass, class, interface method, superclass method, and class method.
- Spring applies the class-level annotation to all public methods of this class that we did not annotate with @Transactional.
- However, if we put the annotation on a private or protected method, Spring will ignore it without an error.

### Q. @Transactional important attribute, theis possible values and uses?
1. Propagation
- Propagation defines how transactions interact with each other. It determines how a method should run within a transactional context, especially when a method is called within another method that has a transaction. Here are the key propagation types:
- REQUIRED (default): If there is an existing transaction, the method will join it. If there is no existing transaction, a new one will be started.
- REQUIRES_NEW: Always starts a new transaction, suspending the current one if it exists.
- NESTED: Starts a new transaction within the current one, creating a savepoint. If the nested transaction rolls back, it doesn't affect the outer transaction.
- SUPPORTS: If there is an existing transaction, the method will join it. If there is no existing transaction, it will run without a transaction.
- NOT_SUPPORTED: The method will not run within a transaction. If there's an existing transaction, it will be suspended.
- MANDATORY: Requires an existing transaction. If there's no transaction, an exception will be thrown.
- NEVER: The method must not run within a transaction. If there's an existing transaction, an exception will be thrown.

2. Isolation
- Isolation determines how and when the changes made in one transaction become visible to other transactions. It helps manage concurrency issues like dirty reads, non-repeatable reads, and phantom reads. Here are the main isolation levels:
- DEFAULT: Uses the default isolation level of the underlying database.
- READ_UNCOMMITTED: Lowest isolation level. Allows reading uncommitted changes made by other transactions (dirty reads).
- READ_COMMITTED: Ensures a transaction can only read committed changes. Prevents dirty reads but still allows non-repeatable reads.
- REPEATABLE_READ: Ensures that if a transaction reads the same row twice, it will see the same data both times. Prevents dirty reads and non-repeatable reads.
- SERIALIZABLE: Highest isolation level. Transactions are executed in a sequential order, effectively serializing them.Prevents dirty reads, non-repeatable reads, and phantom reads, but can significantly impact performance due to locking.

- When you use the @Transactional annotation, you can specify these attributes to control the behavior of your transactions. For example:
```
@Transactional(propagation = Propagation.REQUIRED, isolation = Isolation.READ_COMMITTED)
public void someMethod() {
    // method implementation
}
```
- propagation = Propagation.REQUIRED: The method will join an existing transaction if one exists, or start a new one if not.
- isolation = Isolation.READ_COMMITTED: The method will ensure that it only reads committed changes made by other transactions, preventing dirty reads.

### Important dependencies used in project

1. *Apache Commons*: Libraries from Apache Commons provide reusable components, utilities, and helper classes for various tasks such as string manipulation, collections, and I/O operations.(StringUtils, ArrayUtils, BeanUtils, CommandLineParser)
2. *Slf4j (Simple Logging Facade for Java)*: An abstraction layer for various logging frameworks, allowing developers to plug in the desired logging framework at deployment time without changing the application code.
3. *JUnit*: A widely-used testing framework for Java applications, providing annotations and APIs for writing unit and integration tests to ensure the correctness of the application's behavior.
4. *Mockito*: A mocking framework for Java that allows developers to create mock objects for testing, simulate behavior, and verify interactions between objects in unit tests.
5. *Jackson-Databind* : A core component of the Jackson library used for JSON serialization and deserialization in Java applications, providing support for mapping JSON data to Java objects and vice versa.
6. *Tomcat Embed* : An embedded servlet container provided by Apache Tomcat, which is the default embedded container used by Spring Boot for running web applications.
7. *Oracle JDBC Driver (ojdbc8)*: A JDBC driver for Oracle databases, enabling Spring Boot applications to connect and interact with Oracle databases.
8. *Lombok*: A library that helps reduce boilerplate code in Java by automatically generating common methods like getters, setters, and constructors.
