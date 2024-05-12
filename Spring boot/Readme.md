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
1. *Configuration*
```
package ComponentAnnotation;
 
// Class
@Component
public class College {
 
    // Method
    public void test()
    {
        // Print statement
        System.out.println("Test College Method");
    }
}
```
a. Spring:
In a traditional Spring application, you need to configure your application using XML files or Java-based configuration classes.\
xml
```
<!-- Example of XML configuration -->
<context:component-scan base-package="ComponentAnnotation"/>
```
java
```
// Example of Java-based configuration
@Configuration
public class AppConfig {
@Bean
// Here the method name is the
// bean id/bean name
public College collegeBean(){
	// Return the College object
	return new College();
}
}
```
now to fetch bean
```
public class Main {
 
    // Main driver method
    public static void main(String[] args)
    {
 
        // Use AnnotationConfigApplicationContext
        // instead of ClassPathXmlApplicationContext
        // because we are not using XML Configuration
        ApplicationContext context = new AnnotationConfigApplicationContext(CollegeConfig.class);
 
        // Getting the bean
        College college
            = context.getBean("collegeBean", College.class);
 
        // Invoking the method
        // inside main() method
        college.test();
    }
}
```
b. Spring Boot: \
Spring Boot provides opinionated defaults and auto-configuration, reducing the need for extensive configuration. It uses convention over configuration.
```
// Spring Boot application class (no XML or explicit configuration needed)
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
In Spring boot,there is no need of AppConfig class and dependency can directly be injected using Autowired and @SpringBootApplication will do auto-configuration.\

2. Dependency Management: \
a. Spring: 
In a standard Spring application, you need to manually manage dependencies and versions, which can lead to compatibility issues. \
b. Spring Boot:
Spring Boot uses a "Starter" mechanism to manage dependencies. Starters are pre-packaged sets of dependencies that are commonly used together. Spring Boot's "parent" POM enforces consistent dependency versions.

4. Embedded Server: \
a. Spring:
In traditional Spring applications, you need to deploy your application to an external web server like Tomcat, Jetty, or WildFly. \
b. Spring Boot:
Spring Boot includes an embedded web server (e.g., Tomcat, Jetty, or Undertow) by default, making your application self-contained and reducing the need for external server deployment.

5. Configuration Properties: \
a. Spring:
In Spring, you manage configuration properties through XML or @PropertySource annotations. \
b. Spring Boot:
Spring Boot simplifies property configuration by providing application.properties or application.yml files. You can easily define properties and override them based on profiles or external configuration.

6. Auto-Configuration: \
a. Spring:
In Spring, you need to configure many components manually, such as data sources, security, and view resolvers. \
b. Spring Boot:
Spring Boot's auto-configuration feature automatically configures many common components based on the dependencies you include in your project. For example, *adding spring-boot-starter-data-jpa automatically configures a data source and entity manager*.

7. Convention Over Configuration: \
a. Spring:
Spring follows the principle of "explicit configuration," where you need to provide explicit configuration details for most components. \
b. Spring Boot:
Spring Boot follows the principle of "convention over configuration." It provides sensible defaults, making it easy to get started without extensive configuration.

8. Application Entry Point: \
a. Spring:
In a standard Spring application, you need to manually create a main class and set up an application context. \
```
public class MyApplication {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        // ...
    }
}
```
b. Spring Boot:
Spring Boot simplifies the application entry point using the @SpringBootApplication annotation.
```
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

8. Simplified Testing: \
a. Spring:
In Spring, you often need to configure the Spring TestContext framework manually. \
b. Spring Boot:
Spring Boot provides a @SpringBootTest annotation for integration testing, making it easier to set up and run tests.

### 5. Compare Spring Boot vs Spring MVC?
1. Setup and Configuration:
a. Spring MVC:
Setting up a Spring MVC project involves configuring web.xml, dispatcher servlet, application context, and other configurations.
You need to manage dependencies and configurations manually.
b. Spring Boot:
Setting up a Spring Boot project is streamlined using Spring Initializr or via IDE plugins.
Spring Boot provides sensible defaults and auto-configuration, reducing manual setup. \
Example:For Spring Boot, you can use Spring Initializr (https://start.spring.io/) to generate a project with specific dependencies. For example, including "Web" will set up Spring MVC.

2. Auto-Configuration:
a. Spring MVC:
In Spring MVC, you have to configure many components manually, like ViewResolvers, MessageConverters, etc.
b. Spring Boot:
Spring Boot provides auto-configuration, which automatically configures components based on project dependencies. It reduces the need for manual configuration.
Example:
```
// Spring Boot Application class with @SpringBootApplication annotation
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

3. Embedded Server:
a. Spring MVC:
You need to manually configure and manage an external web server like Tomcat or Jetty.
b. Spring Boot:
Spring Boot includes an embedded server (like Tomcat, Jetty, or Undertow) by default. You don't need to install or configure an external server. \
Example:In Spring Boot, you can run the application directly as a Java application, and it starts the embedded server automatically.

4. Dependency Management:
a. Spring MVC:
You have to manually manage dependencies and versions in your project.
b. Spring Boot:
Spring Boot manages dependencies for you. Starter POMs include compatible versions of various libraries, ensuring they work well together. \
Example:Starter POMs include dependencies like spring-boot-starter-web for web applications. You don't need to specify versions; Spring Boot takes care of it.

5. Production-Ready Features:
a. Spring MVC:
In Spring MVC, you need to manually configure features like health checks, metrics, and other production-ready features.
b. Spring Boot:
Spring Boot Actuator provides built-in tools for monitoring and managing applications in production. \
Example:With Spring Boot, adding production-ready features is as simple as including the spring-boot-starter-actuator dependency.

6. Simplified Development:
a. Spring MVC:
You need to configure various aspects like database connection, logging, and security manually.
b. Spring Boot:
Spring Boot provides sensible defaults. For example, it auto-configures a DataSource if you have the necessary dependencies.
Example:yaml
```
# application.properties or application.yml
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
```

7. Microservices Support:
a. Spring MVC:
While Spring MVC can be used in microservices, it doesn't provide specific features for microservices architecture.
b. Spring Boot:
Spring Boot is well-suited for building microservices. It integrates well with Spring Cloud for features like service discovery, circuit breaking, etc. \
Example:Using Spring Boot with Spring Cloud, you can easily create microservices that register with a service registry for discovery.

8. Ease of Testing:
a. Spring MVC:
Testing Spring MVC applications often requires setting up various configurations for the test environment.
b. Spring Boot:
Spring Boot simplifies testing by providing annotations like @SpringBootTest for integration tests. \
Example:
```
@SpringBootTest
public class MyIntegrationTest {
    // Your test code here
}
```

### 6. What is @SpringBootApplication,it's significance and what will happen if we don't use it?
- The @SpringBootApplication annotation is a crucial component in a Spring Boot application.
- It combines several annotations into a single, convenient package and is often found at the entry point of a Spring Boot application class.
- Why Do We Need @SpringBootApplication?
1. *Simplification*: Spring Boot's goal is to simplify the configuration and setup of Spring applications. Without @SpringBootApplication, you'd have to apply multiple annotations separately, which can be tedious and error-prone.
2. *Auto-Configuration*: It triggers Spring Boot's auto-configuration mechanism, which automatically configures various aspects of your application based on your project's dependencies. This helps in reducing manual configuration efforts.
3. *Component Scanning*: It enables component scanning, allowing Spring to discover and register beans, controllers, services, and other components within your application.
- What Happens If We Don't Use @SpringBootApplication?
If you don't use @SpringBootApplication, your Spring Boot application may still work, but you'll need to do much more manual configuration and setup. \
You'll miss out on the benefits of auto-configuration and component scanning, making your application less efficient and more prone to configuration errors.
- Code Example: \
Let's see how @SpringBootApplication simplifies the setup of a Spring Boot application with a simple example.
a. *Without @SpringBootApplication*:
```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@EnableAutoConfiguration
@ComponentScan
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
b. *With @SpringBootApplication*:
```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

### 7.Explain @Component, @Service, @Repository, @Configuration, @EnableAutoConfiguration, @ComponentScan, @EntityScan, @Transient, @Bean.
1. *@Component* :
- generic stereotype annotation for any spring-managed component.
- indicates that a class is a Spring component and it can be auto-detected during classpath scanning.
- tyically used for creating beans without any specific stereotype (e.g.@Service,@Repository) or to marka custom class as a Spring bean.
```
@Component
 public class ComponentDemo {
    public void demoFunction()
    {
        System.out.println("Hello GeeksForGeeks");
    }
}
```
2. *@Service* :
- specialization of @Component and is typically used to annotate service classes.
- these classes hold the business logic and are often used in the service layers of an application.
- automatically discovered and registered as Spring beans
```
@Service
@Transactional
public class UserServiceImpl implements IUserService {
	@Autowired
	private SellerRepository sellerRepo;

	public Seller findSellerByBuisenessName(String businessName) {
		return sellerRepo.findByBusinessName(businessName)
				.orElseThrow(() -> new UserHandlingException("Invalid Buiseness Name..!"));
	}
}
```
3. *@Repository* :
- another specialization of @Compoent and is typically used to annotate repository (data access) classes.
- used to indicate that the class provides the mechanism for storage, retrieval, update, delete and search operation on objects.
- often work with databases and Spring's Data Access/Integration technologies.
```
 @Repository
public interface CartRepository extends JpaRepository<Cart, Integer> {

	Optional<Cart> findByUserIdAndProductId(Integer userId, Integer productId);
	
	@Query("select distinct c.sellerId from Cart c")
    int[] findDistinctSellerId();
	
	@Query("select c from Cart c where c.userId=:uid and c.sellerId=:sid")
	List<Cart> findAllByUserIdAndSellerId(@Param("uid") Integer userId, @Param("sid") int sellerId);
	
    List<Cart> findAllByUserIdOrderByCreatedDateDesc(Integer userId);
}
``` 
4. *@Configuration* :
- The @Configuration annotation is a Spring framework annotation that indicates that a class defines one or more Spring beans or configuration methods.
- It is used to define configuration classes that provide bean definitions or configuration for the Spring container.
- Without @Configuration, the Spring container may not recognize the class as a configuration source, and you won't be able to define beans or configure components within it.
```
@Configuration
public class MyConfiguration {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```
In this example, MyConfiguration is marked as a configuration class, and it defines a bean named myBean using the @Bean annotation.

5. *@EnableAutoConfiguration* :
- The @EnableAutoConfiguration annotation is a Spring Boot-specific annotation that enables Spring Boot's auto-configuration feature.
- It automatically configures various components and settings based on the project's dependencies, reducing manual configuration efforts.
- Spring Boot's auto-configuration simplifies the setup of a Spring Boot application by providing sensible defaults. Without it, you would need to configure many components manually.
```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;

@EnableAutoConfiguration
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
In this example, @EnableAutoConfiguration is used to enable Spring Boot's auto-configuration for the application.

6. *@EntityScan* :
- When writing our Spring application we will usually have entity classes – those annotated with @Entity annotation. We can consider two approaches to placing our entity classes:
a. Under the application main package or its sub-packages.
b. Use a completely different root package .
- In the first scenario, we could use @EnableAutoConfiguration to enable Spring to auto-configure the application context.
- In the second scenario, we would provide our application with the information where these packages could be found. For this purpose, we would use @EntityScan.
- @EntityScan annotation is used when entity classes are not placed in the main application package or its sub-packages. In this situation, we would declare the package or list of packages in the main configuration class within @EntityScan annotation.
- This will tell Spring where to find entities used in our application:
```
@Configuration
@EntityScan("com.baeldung.demopackage")
public class EntityScanDemo {
    // ...
}
```
- We should be aware that using @EntityScan will disable Spring Boot auto-configuration scanning for entities.

7. *@ComponentScan* :
- Similar to @EntityScan and entities, if we want Spring to use only a specific set of bean classes, we would use @ComponentScan annotation.
- It’ll point to the specific location of bean classes we would want Spring to initialize.
- This annotation could be used with or without parameters. Without parameters, Spring will scan the current package and its sub-packages, while, when parameterized, it’ll tell Spring where exactly to search for packages.
- Concerning parameters, we can provide a list of packages to be scanned (using basePackages parameter) or we can name specific classes where packages they belong to will also be scanned (using basePackageClasses parameter).
```
@Configuration
@ComponentScan(
  basePackages = {"com.baeldung.demopackage"}, 
  basePackageClasses = DemoBean.class)
public class ComponentScanExample {
    // ...
}
```
In this example, @ComponentScan is used to specify that Spring should scan the com.baeldung.demopackage package and its sub-packages for components.

### 8. What is Auto Configuration?
- Auto Configuration is a fundamental feature of Spring Boot. 
- It is a mechanism that automatically configures various components and settings within your Spring Boot application based on the libraries and dependencies you have in your project. 
- The primary goal of auto configuration is to reduce the need for manual configuration, making it easier to set up and run Spring Boot applications.
- Auto Configuration is automatically enabled in Spring Boot applications by default. There's typically no need to enable it explicitly; it's an integral part of the Spring Boot framework.
- For example, if you include the spring-boot-starter-data-jpa dependency, Spring Boot will configure a data source and entity manager.

### 9. What is an embedded server? Why is it important?
- An embedded server, such as Tomcat or Jetty, is a web server that is bundled within the application.
- Spring Boot's embedded servers simplify deployment because you don't need to separately install and configure a server.
- It's especially important for creating self-contained, executable JAR files.

### 10. What is the default embedded server with Spring Boot? What is the default port of tomcat in spring boot?
- The default embedded server with Spring Boot is Tomcat.
- It's included by default when you use Spring Boot for web applications.
- The default port of the tomcat server-id 8080. It can be changed by adding sever.port properties in the application.property file.

### 11. What are the other embedded servers supported by Spring Boot?
- Spring Boot supports several embedded servers, including Jetty, Undertow, and more. You can choose a different server by adding the corresponding dependency to your project.

### 12. What are Starter Projects?Give examples of few important starter projects.
- Starter Projects are pre-configured templates that provide a baseline setup for different types of applications. They include specific dependencies and configurations to kickstart your development.
1. spring-boot-starter-web: For building web applications.
2. spring-boot-starter-data-jpa: For data access with JPA.
3. spring-boot-starter-security: For adding security features.
4. spring-boot-starter-test: For testing with JUnit and other testing frameworks.

### 14. What is POM Parent?
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

-----
*for better understanding*

In layman's terms, think of Spring Initializer as a "recipe generator" for building Spring Boot applications. \
Instead of starting from scratch and gathering all the ingredients and cooking instructions yourself, you provide some basic information, and Spring Initializer gives you a ready-to-use recipe (project) that you can start working on immediately. \

Here's how it works: \
[*Visit the Spring Initializer Website*](https://start.spring.io/) \
You go to the Spring Initializer website, which is like an online kitchen for building Spring Boot applications. \

*Choose Your Ingredients (Project Options)*: \
You select the ingredients you want for your project. These ingredients include things like the programming language (Java or Kotlin), the Spring Boot version, and the type of project (e.g., web application, data access, etc.). \

*Customize Your Recipe (Project Metadata)*: \
You can add some additional information, like the name of your project and the package name. This is like naming your dish and specifying how you want it to be served. \

*Click "Generate"*: \
After choosing your ingredients and customizing your recipe, you click a button called "Generate." \

*Get Your Recipe (Download the Project)*: \
Spring Initializer prepares your project based on your choices and gives you a downloadable package. This package contains all the files and settings needed to start your Spring Boot project. \

Here's a simplified example of how you might use Spring Initializer: \
Suppose you want to create a Spring Boot web application using Java. You visit Spring Initializer, choose Java as the programming language, select the latest Spring Boot version, name your project "MyWebApp," and click "Generate." Spring Initializer then provides you with a ZIP file containing a project folder with all the necessary files and dependencies pre-configured. \

*Why Do We Need Spring Initializer?* \
Spring Initializer serves several important purposes: \
*Saves Time*: Creating a Spring Boot project from scratch can be time-consuming and error-prone. Spring Initializer automates this process, saving you time and effort. \
*Ensures Best Practices*: Spring Initializer generates projects that adhere to Spring Boot best practices, ensuring that you start with a solid foundation. \
*Dependency Management*: It simplifies dependency management by including the necessary libraries and version control. You don't need to manually search for dependencies and add them to your project. \
*Streamlines Configuration*: Spring Initializer sets up essential configuration files (like application.properties or application.yml) with sensible defaults. \

*If you don't use Spring Initializer, you'd need to perform the following manual steps to set up a Spring Boot project*:
Create a new project directory. \
Set up the project build system (Maven or Gradle) and create the necessary build configuration files. \
Manually add dependencies to your build file for Spring Boot, libraries, and frameworks you plan to use. \
Create the project structure, including main and test source code directories. \
Write configuration files for Spring Boot, such as application.properties or application.yml. \
Configure and set up your project's packaging, naming conventions, and other project-specific settings. \
Manually manage the initialization of the Spring Boot application context and any additional configurations. \

By using Spring Initializer, you skip these manual steps and start with a fully configured and structured project, allowing you to focus on writing your application's business logic rather than dealing with project setup and boilerplate code.

-----

### 18. What is application.properties?
- application.properties is a configuration file commonly used in Spring Boot applications to manage application-specific settings and properties.
- It plays a crucial role in configuring various aspects of your Spring Boot application without modifying the source code.
- You can customize properties related to database configuration, logging levels, server settings, external service URLs, and any other configuration needed for your application.
- This file is especially useful for externalizing configuration(another way is application.yml) from your codebase, making it easier to modify settings without recompiling the application.Spring Boot will automatically load these properties when the application starts.

### 19.Why is application.properties Required?
- *External Configuration*: It allows you to configure your application externally. Instead of hardcoding configuration values within your code, you can specify them in the application.properties file. This makes it easier to change settings without modifying your code, which is crucial for configuring applications across different environments (e.g., development, testing, production).
- *Maintainability*: Separating configuration from code improves the maintainability of your application. You can change configuration values without needing to recompile the application, making it more flexible and adaptable.
- *Profile Management*: Spring Boot supports profiles, which enable you to define different configurations for different environments (e.g., application-dev.properties for development and application-prod.properties for production). By using application.properties along with profiles, you can manage configuration settings for various scenarios efficiently.

-----

Here's an example of an application.properties file and how you can use its properties in a Spring Boot application code. \

Example application.properties file:
```
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=myuser
spring.datasource.password=mypassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Server Configuration
server.port=8080

# Logging Configuration
logging.level.org.springframework=INFO
logging.level.com.myapp=DEBUG

# Custom Application Property
myapp.api.key=secretapikey
```

Now, let's see how you can use these properties in your Spring Boot application code: \

*Creating a Configuration Class*: \
You can create a configuration class in your Spring Boot project to access and use these properties. Here's an example: \
```
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Value("${spring.datasource.url}")
    private String databaseUrl;

    @Value("${spring.datasource.username}")
    private String databaseUsername;

    @Value("${server.port}")
    private int serverPort;

    @Value("${myapp.api.key}")
    private String apiKey;

    public String getDatabaseUrl() {
        return databaseUrl;
    }

    public String getDatabaseUsername() {
        return databaseUsername;
    }

    public int getServerPort() {
        return serverPort;
    }

    public String getApiKey() {
        return apiKey;
    }
}
```

In this configuration class, we use the *@Value* annotation to inject property values from application.properties into instance variables. For example, *@Value("${spring.datasource.url}")* injects the spring.datasource.url property value into the databaseUrl variable. \

*Using Configuration Properties in a Service or Controller*: \
You can then use these properties in your service or controller classes as needed. Here's an example:
```
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    private final AppConfig appConfig;

    @Autowired
    public MyController(AppConfig appConfig) {
        this.appConfig = appConfig;
    }

    @GetMapping("/api/config")
    public String getConfig() {
        return "Database URL: " + appConfig.getDatabaseUrl() + "\n"
               + "Database Username: " + appConfig.getDatabaseUsername() + "\n"
               + "Server Port: " + appConfig.getServerPort() + "\n"
               + "API Key: " + appConfig.getApiKey();
    }
}
```
In this controller class, we inject the AppConfig bean and use its methods to retrieve and display the configured properties. \

By using @Value annotations and a configuration class, you can access and use properties defined in application.properties throughout your Spring Boot application code. This allows you to centralize and manage configuration settings easily, making your application more flexible and maintainable.

-----

### 20.What is Application.yaml?
- application.yaml (or application.yml) is an alternative configuration file format used in Spring Boot applications, alongside the more common application.properties file.
- Both formats serve the same purpose: configuring your Spring Boot application.
- However, they have different syntax and features, allowing you to choose the one that suits your preferences and needs.

### 21.How Application.yaml is different from application.properties?
1. *YAML vs. Properties*:
- application.properties uses a key-value pair format with properties separated by equal signs (=).
- application.yaml uses a YAML (YAML Ain't Markup Language) format, which is a human-readable data serialization format. It uses indentation to represent data structures.

2. *Readability*:
application.yaml is often considered more readable and user-friendly, especially for complex configurations with nested properties and lists.
YAML's indentation-based structure makes it easy to represent hierarchical data.

3. *Syntax*:
In application.properties, you set properties like this:
```
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
myapp.api.key=secretapikey
```
In application.yaml, you use YAML syntax, which looks like this:
```
server:
  port: 8080
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
myapp:
  api:
    key: secretapikey
```

4. *Profiles*:
- Both formats support profiles, allowing you to define different configurations for different environments (e.g., application-dev.properties or application-dev.yaml for development).

5. *Nested Properties*:
YAML is often more concise and readable for defining nested properties:
```
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
```
In application.properties, nested properties require repetition of prefixes:
```
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```
Here's an example of how the same configuration could be represented in both formats: \

application.properties:
```
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
myapp.api.key=secretapikey
myapp.supported-languages[0]=English
myapp.supported-languages[1]=Spanish
myapp.supported-languages[2]=French
myapp.description=This is a multiline \
  description for my app.
```
application.yaml:
```
server:
  port: 8080
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
myapp:
  api:
    key: secretapikey
  supported-languages:
    - English
    - Spanish
    - French
  description: |
    This is a multiline
    description for my app.
```

### 22. How can you add custom application properties using Spring Boot?
- You can add custom application properties in the application.properties file or a dedicated custom properties file and access them using Spring's @Value annotation or the Environment object.

### 23. What is @ConfigurationProperties?
- @ConfigurationProperties is an annotation in Spring Boot that allows you to bind properties defined in configuration files, such as application.properties or application.yml, to Java objects.
- It provides a convenient way to externalize configuration settings and inject them into your Spring components.

-----

Suppose you have a Spring Boot application that connects to a database, and you want to externalize the database configuration settings using *@ConfigurationProperties*. \

1. Define a Configuration Class:
   
Create a Java class to represent the configuration properties. The class should have fields corresponding to the properties you want to externalize. For example: \
```
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "database")
public class DatabaseConfig {
    private String url;
    private String username;
    private String password;
    // getters and setters
}
```
In this example, we use the @ConfigurationProperties annotation to specify that this class will be used to bind properties with the database prefix from the configuration files.

2. Configure application.properties or application.yml:

Define the properties you want to externalize in your configuration file (application.properties or application.yml). Make sure to use the specified prefix ("database" in this case):
```
database.url=jdbc:mysql://localhost:3306/mydb
database.username=myuser
database.password=mypassword
```

3. Use the Configuration Properties in Your Application:

You can now use the DatabaseConfig bean in your application components, such as services or controllers:
```
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    private final DatabaseConfig databaseConfig;

    @Autowired
    public MyController(DatabaseConfig databaseConfig) {
        this.databaseConfig = databaseConfig;
    }

    @GetMapping("/db-config")
    public String getDatabaseConfig() {
        return "Database URL: " + databaseConfig.getUrl() + "\n" +
               "Database Username: " + databaseConfig.getUsername() + "\n" +
               "Database Password: " + databaseConfig.getPassword();
    }
}
```
In this controller, we inject the DatabaseConfig bean and use its getters to access the database configuration properties. \

By using @ConfigurationProperties, you've externalized your database configuration, achieved type safety, and organized your code in a cleaner way. Any changes to the configuration can be made in the application.properties or application.yml file without modifying the Java code, making your application more flexible and easier to manage.

-----

### 24.How  @ConfigurationProperties different from @Configuration in spring boot?
1. *@Configuration*:
- @Configuration is used to mark a class as a configuration class.
- Configuration classes are typically used to define Spring Beans, and they are a way to configure the Spring application context.
- You can define methods within a @Configuration class annotated with @Bean to create and configure Spring Beans.
- It is used to define and configure beans, manage application context, and set up other configuration-related tasks.
- Configuration classes are typically used for Java-based configuration.
```
@Configuration
public class MyConfiguration {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```
2. *@ConfigurationProperties*:
- @ConfigurationProperties is used to bind external configuration properties to Java objects.
- It is primarily used for externalizing configuration settings from your code and injecting them into Spring components as Java objects.
- You annotate a Java class with @ConfigurationProperties, specify a prefix for the properties you want to bind, and define fields within the class corresponding to the properties.
- This annotation provides type-safe binding of properties and is useful when you want to centralize and manage configuration properties.
```
@Component
@ConfigurationProperties(prefix = "database")
public class DatabaseConfig {
    private String url;
    private String username;
    private String password;
    // getters and setters
}
```
- In summary, @Configuration is used for configuring beans and the Spring application context, while @ConfigurationProperties is used for externalizing configuration properties and binding them to Java objects. - They serve different purposes within a Spring Boot application, and you may use them in different scenarios based on your requirements.

### 25. Can @ConfigurationProperties be used with @Value?
- *@ConfigurationProperties* and *@Value* are two distinct mechanisms for retrieving configuration properties in a Spring Boot application, and they are typically used independently.
- However, you can technically use them together in specific scenarios when needed.
- Here's how you can use @ConfigurationProperties with @Value:
- *Using @ConfigurationProperties for Structured Configuration*: \
- You use @ConfigurationProperties to bind a group of related configuration properties to a Java object. This is especially useful when you want to manage structured or complex configurations.
```
@Component
@ConfigurationProperties(prefix = "myapp")
public class MyAppConfig {
    private String apiKey;
    private String serviceUrl;
    // getters and setters
}
```
- In this example, we bind properties with the prefix "myapp" to the MyAppConfig class.
- *Using @Value to Access Specific Properties*:
- You use @Value to inject a specific configuration property into a field or method parameter when you only need that property in a particular part of your code.
```
@Component
public class MyService {
    @Autowired
    private MyAppConfig myAppConfig; // Inject the entire configuration

    @Value("${myapp.apiKey}")
    private String apiKey; // Use @Value to access a specific property

    public void doSomething() {
        // Use myAppConfig to access the entire configuration object
        // Use apiKey to access the specific property
    }
}
```
- In this example, we inject the entire "myapp" configuration using @Autowired and MyAppConfig, and then we use @Value to inject the "myapp.apiKey" property directly into the apiKey field.
- Using @ConfigurationProperties with @Value in this way allows you to combine structured configuration (with @ConfigurationProperties) and access to specific properties (with @Value) as needed in your code.
- However, keep in mind that it's generally more common to choose one of these mechanisms based on your specific use case. @ConfigurationProperties is preferred for structured configurations, while @Value is suitable when you only need individual properties in isolated parts of your code.

### 26. What is a Profile and why is it used?
- A profile in Spring Boot allows you to define different sets of configurations for different environments or scenarios. It helps manage application behavior in various contexts (e.g., development, production).
- While developing the application we deal with multiple environments such as dev, QA, Prod, and each environment requires a different configuration.
- For eg., we might be using an embedded H2 database for dev but for prod, we might have proprietary Oracle or DB2. Even if DBMS is the same across the environment, the URLs will be different.
- To make this easy and clean, Spring has the provision of Profiles to keep the separate configuration of environments.

### 27. How do you define beans for a specific profile?
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

### 28. How do you create application configuration for a specific profile?
- You can create separate configuration files for different profiles by naming them as application-{profile}.properties or application-{profile}.yml. Spring Boot will load the appropriate configuration based on the active profile.
- For the dev profile, create a file named application-dev.properties or application-dev.yml (if you prefer YAML configuration).
- For the prod profile, create a file named application-prod.properties or application-prod.yml.
- These files should be located in the same directory as your application.properties or application.yml file.

### 29. How do you have different configuration for different environments?
- You can create separate configuration files for different environments (e.g., application-dev.properties, application-prod.properties) and activate the appropriate profile when starting the application. Spring Boot will load the corresponding configuration.

### 30. What is Spring Boot Actuator?
- Spring Boot Actuator is a set of production-ready features and tools provided by Spring Boot for monitoring and managing your application in a production environment.
- It's like having a dashboard for your Spring Boot application that gives you insights into how your application is performing, its health, and various runtime metrics.

### 31.Why Spring boot actuator is required?
1. *Monitoring and Management*: Spring Boot Actuator helps you monitor the health, performance, and behavior of your application in real-time. You can check if your application is running properly, detect issues, and manage its components without interrupting service.
2. *Debugging and Troubleshooting*: It provides essential information about the application's internals, such as environment properties, memory usage, and configuration. This information is invaluable for debugging and troubleshooting issues in production.
3. *Security*: Spring Boot Actuator offers security measures to restrict access to sensitive endpoints, ensuring that only authorized personnel can access and manage your application's internals.
4. *Operational Insights*: It collects and exposes metrics and statistics about your application, which can help operations teams gain insights into resource usage, bottlenecks, and overall system health.
5. *Integration with Monitoring Tools*: Spring Boot Actuator seamlessly integrates with popular monitoring and management tools like Prometheus, Grafana, and Spring Cloud Sleuth, making it easier to manage your application in a larger ecosystem.

### 32.How to implement Spring boot actuator?
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

### 33. How do you monitor web services using Spring Boot Actuator?
- You can use Actuator's built-in endpoints to monitor web services. For example, the /actuator/health endpoint provides information about the application's health, and /actuator/metrics offers various metrics.

### 34. How do you find more information about your application environment using Spring Boot?
- Spring Boot Actuator provides the /actuator/env endpoint, which displays environment properties, including application properties and system properties.

### 35.How to enable debugging log in the spring boot application?
- Debugging logs can be enabled in three ways -
1. We can start the application with --debug switch.
2. We can set the logging.level.root=debug property in application.property file.
3. We can set the logging level of the root logger to debug in the supplied logging configuration file.

### 36. What is a CommandLineRunner?
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
These explanations and examples should help you understand Spring Boot concepts and features in a practical and straightforward way for your interview preparation.

### 37. What is a EnableTransactionManagement and Transactional annotation?
- The *@EnableTransactionManagement* annotation and *@Transactional* annotation work together to manage transactions in a Spring application, but they serve different purposes:
- **@EnableTransactionManagement**: This annotation is used at the configuration level (typically on a @Configuration class) to enable Spring's annotation-driven transaction management capability within the application. It activates Spring's ability to interpret @Transactional annotations and manage transactions accordingly.
- **@Transactional**: This annotation is applied at the method level or on a class, indicating that the methods (or all methods within the annotated class) should be wrapped in a transaction. It defines the scope of a single database transaction. This annotation provides metadata that Spring uses to create a transactional proxy around the annotated method or class to manage transactional behavior.
- In essence, @EnableTransactionManagement enables Spring to recognize @Transactional annotations within the application and manage transactions based on the specified semantics.

### 38.Explain what isolation & propagation parameters are for in the @Transactional annotation via real-world example?
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

----
*for better understanding*

A practical example of where a new transaction will always be created when entering the provideService routine and completed when leaving:
```
public class FooService {
    private Repository repo1;
    private Repository repo2;

    @Transactional(propagation=Propagation.REQUIRES_NEW)
    public void provideService() {
        repo1.retrieveFoo();
        repo2.retrieveFoo();
    }
}
```

- Had we instead used REQUIRED, the transaction would remain open if the transaction was already open when entering the routine. Note also that the result of a rollback could be different as several executions could take part in the same transaction.

- We can easily verify the behaviour with a test and see how results differ with propagation levels:

```
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations="classpath:/fooService.xml")
public class FooServiceTests {

    private @Autowired TransactionManager transactionManager;
    private @Autowired FooService fooService;

    @Test
    public void testProvideService() {
        TransactionStatus status = transactionManager.getTransaction(new DefaultTransactionDefinition());
        fooService.provideService();
        transactionManager.rollback(status);
        // assert repository values are unchanged ... 
}
```
With a propagation level of
- *REQUIRES_NEW*: we would expect fooService.provideService() was NOT rolled back since it created its own sub-transaction.
- *REQUIRED*: we would expect everything was rolled back and the backing store was unchanged.

### 39.Difference between @Controller and @RestController?
- Spring 4.0 introduced the @RestController annotation in order to simplify the creation of RESTful web services. It’s a convenient annotation that combines @Controller and @ResponseBody, which eliminates the need to annotate every request handling method of the controller class with the @ResponseBody annotation.
1. @Controller -
- a specialization of the @Component class, which allows us to auto-detect implementation classes through the classpath scanning.
- common annotation used to create Spring MVC controllers that are responsible for processing web requests.
- typically used in traditional web appls where the response is usually a web page (HTML view).
- these controllers generally return views(HTML pages) that are rendered by a templating engine (e.g.,Thymeleaf,JSP) and sent to the client's web browser.
- We typically use @Controller in combination with a @RequestMapping annotation for request handling methods.
```
@Controller
@RequestMapping("/books")
public class SimpleBookController {
    @GetMapping(value = "/abc.do")
    public ModelAndView getBook(@RequestParam(value = "xyz",required = true) String xyz,HttpServletRequest request) {
        ModelAndView modelAndView = new ModelAndView("login");
        // logic
        return modelAndView;
    }
}
```
```
@Controller
@RequestMapping("books")
public class SimpleBookController {

    @GetMapping("/{id}", produces = "application/json")
    public @ResponseBody Book getBook(@PathVariable int id) {
        return findBookById(id);
    }

    private Book findBookById(int id) {
        // ...
    }
}
```
- We annotated the request handling method with @ResponseBody. This annotation enables automatic serialization of the return object into the HttpResponse.

2. @RestController -
- @RestController is a specialized version of the controller.
- It is a combination of behaviours of a Controller and ResponseBody.
- When we use this Annotation, the response is JSON or XML. Because of this, the Controller is not in charge of providing any viewpoint to the user.
- Every request handling method of the controller class automatically serializes return objects into HttpResponse.
```
@RestController
@RequestMapping("books-rest")
public class SimpleBookRestController {
    
    @GetMapping("/{id}", produces = "application/json")
    public Book getBook(@PathVariable int id) {
        return findBookById(id);
    }

    private Book findBookById(int id) {
        // ...
    }
}
```

### 40.How does @Compoent and @Service annotation works internally?what difference will it make if we use @Component instead of @Service or vice versa?
- Internally when Spring scans the components in application context,it identifies classed annotated with @Component, @Service, @Repository etc. and registers them as beans in the Spring IOC container.
- These beans can then be injected into other components,and their lifecycle is managed by the container.

 *Differences* :
 1. Expressiveness and Semantic Clarity : @Service provides a more expressive and semantic meaning to a class, indicating that it is a service component.This can improve code readability and make the purpose of the class more apparent.
 2. Component Scannig : Both annotations trigger component scanning, and, from a functionality standpoint, there is no difference between using @Component and @Service.The difference lies in the intended use and the clarity of the code.
 3. Consideration for the layered architecture : @Service is often used in the service layer of a typical layered architecture (like MVC),making it a good fit for services with business logic.@Component is more generic and can be used for any component.

- Both annotation work similarly and using one over the other doesn't affect the core functionality of the Spring.The choice between both annoation depends on your preference for semantic clarity and the intended use of annotated class in your application architecture.
- They are interchangeable from a functional standpoint,and use of one above other is matter of convention and redability.


### 1. Can you explain the difference between JPA and JDBC?
1. *JDBC (Java DataBase Connectivity)* – is an API for Java applications that defines how a client may communicate with a database.
- The API uses abstractions close to the relational database domain: Connection, Statement, ResultSet.
- It is a low-level database access framework that allows developers to execute SQL statements and fetch results in a table-like format – ResultSet.
- We can describe its workflow in the following steps:
1. Connect to the database;
2. Fetch the data from the database in the form of a result set;
3. Loop through every record in the result set, create a Java class instance for each record and fill its properties with the record values.
- While working with DB using JDBC, we should write a lot of similar boilerplate code to transform records into Java objects.
- Let's assume that we have a DB table containing records about users: their first and last name and an ID – a unique identifying number.
- To fetch this data to the application, we should do something like this:
```
try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD)) { 
    Statement statement = connection.createStatement(); 
    ResultSet resultSet = statement.execute(SELECT * FROM user); 
    List<User> users = new ArrayList<>(); 
    while (resultSet.next()) { 
        String id = resultSet.getLong("user_id"); 
        String firstName = resultSet.getString("first_name"); 
        String lastName = resultSet.getString("last_name"); 
        users.add(new User(id, firstName, lastName)); 
    } 
} catch (SQLException sqlException) { 
    //... 
}
```
- To reduce the amount of boilerplate code, frameworks that automated this routine work using "mappings" from DB tables to Java objects appeared.
- First, there were text files (usually XML) that specified which class was mapped to which table and which attribute was mapped to which column.
- Then developers started using annotations right in Java classes to specify these mappings.
- There is how Object-Relational mapping (ORM) frameworks appeared.

2. JPA is a specification for ORM frameworks in the Java world.
- "JPA" stands for Jakarta (formerly Java) Persistence API.
- This API provides a higher level of abstraction than JDBC.
- JPA allows us not only to interact with the database but to map records from a database directly to java objects without any manual manipulations from the developer side.
- The API's essential class is an EntityManager responsible for executing queries and transforming relational data into Java objects.
- All we need to do is to create a class, map it to a DB table and then pass it as a parameter to the EntityManager along with the query. \
Our User class will look like this:
```
@Entity 
@Table(name = "user") 
public class User { 
    @Id 
    @Column(name = "user_id", nullable = false) 
    private Long id; 
 
    @Column(name = "first_name") 
    private String firstName; 
 
    @Column(name = "last_name") 
    private String lastName; 

    //getters and setters are omitted
}
```
- Now, we need to write less code to complete the same task as was shown earlier with JDBC:
```
entityManager.getTransaction().begin(); 

TypedQuery<User> query = entityManager.createQuery( 
"SELECT u FROM User u", 
                User.class); 
List<User> users = query.getResultList(); 

entityManager.getTransaction().commit(); 
entityManager.close();
```
We also need to mention that not every ORM implements JPA specification. BlazeDS or MyBatis are such examples.

### 2. What is the difference between JPA and Hibernate?
1. JPA is a specification. In fact, it is a set of interfaces, and vendors provide actual implementations.
2. Hibernate from RedHat is the most popular implementation in the Java world now.
3. There exist other JPA implementations, e.g., EclipseLink or Apache OpenJPA.
4. Each of them must comply with the JPA specification.
5. Apart from this, some of them usually provide vendor-specific APIs not described in the spec.

### 3.Name the main JPA objects
In the JPA specification, there are the following main objects:
1. *Entity*
– a class that is mapped to a database table. Its fields correspond to the columns of the table. The declaration of a regular JPA entity looks like this:
```
@Entity  
public class User {  
    @Id  
    private UUID id;  

    private String firstName;
    private String lastName; 

   //getters and setters are omitted  
}
```
 2. *MappedSuperclass*
– a class that declares common attributes for entities. We use this class to build an entity hierarchy to reuse common attributes.
- Each table associated with an entity from the hierarchy in the database will contain all fields from the MappedSuperclass entity and its descendants.
- As an example, for the following class hierarchy:
```
@MappedSuperclass  
public class Person {  
    @Id  
    private UUID id;  

    private String firstName;  
    private String lastName; 

    //getters and setters are omitted  
}  
@Entity  
public class User extends Person {  

    private String username;  
    private String bio; 

   //getters and setters are omitted  
}
``` 
- We'll need to create a table with columns id, firstname, lastname, username, and bio.

3. *Embeddable*
– a class that we can embed into other entities.
- If we need to treat a pack of fields as one entity and reuse it in various entities, then an embeddable class is what we need.
- For example, we want to store an address for different entities: user, client, etc. We could use inheritance, but for this case, the composition is preferable:
```
@Embeddable  
public class Address {  

    public String country;  
    public String city;  
    public String street;  
    public String building;  

    //getters and setters are omitted  
}  

@Entity  
public class User {  
    @Id  
    @Column(name = "id", nullable = false)  
    private UUID id;  

    private String firstName;  
    private String lastName;  
    
    @Embedded  
    private Address address;  

    //getters and setters are omitted  
}
```  
- For the User entity, we'll need to create a table with columns id, firstname, lastname, country, city, street, and building. When we fetch the User from this table, we can use their address as a separate object at once.

4. *EntityManager*
– a facility that allows us to manage the lifecycle of the JPA entity instance.
- EntityManager API is a part of the JPA specification.
- We can create, read, update or delete an entity from a database by using it.
- EntityManager allows us to execute SQL queries to select entities.
- Also, we can use a special query language - JPQL – to fetch data.
*JPQL is similar to SQL but uses classes and attributes in queries instead of tables and columns*.
- Here is an example of EntityManager usage to fetch data:
```
EntityManagerFactory entityManagerFactory = Persistence.createEntityManagerFactory("default"); 
EntityManager entityManager = entityManagerFactory.createEntityManager(); 
entityManager.getTransaction().begin(); 

TypedQuery<User> query = entityManager.createQuery ( 
        "SELECT u FROM User u WHERE u.address.country='US'", 
        User.class
); 

List<User> users = query.getResultList(); 
entityManager.getTransaction().commit(); 
entityManager.close();
``` 

5. *Session*
– the Hibernate-specific interface that extends the EntityManager.
- All methods defined by the EntityManager are available in the Hibernate Session.
- Many other methods in it are unique to Hibernate, e.g., isDirty(), evict(), cancelQuery() and so on...
  
- Then, you may have a reasonable question: "In which cases is it better to use EntityManager, and in which cases is Session"?
- I will quote Emmanuel Bernard, a data architect on the JBoss Hibernate team. He gives the following answer:
"We encourage people to use the EntityManager. From a team point of view, we wish we had only one API. We are trying to push into the standard as much as we can.
If we could somehow merge or deprecate the Session in the future, we would do it, but people still use some stuff that is not in the EntityManager, and we don't want to just break everybody's application just for the fun of it."
- So, try to use EntityManager whenever it's possible, and when you have no choice but to use Session, unwrap it from the EntityManager:
```
Session session = entityManager.unwrap(Session.class);
``` 

### 4. Which association types and mappings could you specify?
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
- For the latter, we should always keep in mind the limitations of the database side.
- Thus, when we define a bi-directional association, we should know which side of it is the "owning" one.
- An association's "owning" side is responsible for keeping the reference.
- The corresponding table will have the reference column and foreign key constraint.
- The "owning" side reference must be populated.
- Otherwise, the association will not be stored.
- For the example above, if we add a Post instance to the User.posts collection and save the User entity, the association won't be saved.
- But if we assign the Post.user field, everything will be OK.

NOTE: To quickly figure out which side is the "owning" one, just look at the annotation on the reference field. \
If there is the mappedBy attribute – this is the inverse side of the association; otherwise – the owning one.

### 5. Entity ID, what is it?
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

### 6. What does the hbm2ddl.auto/ddl-auto property stand for?
- In fact, it is a single property, but it has two names. The first one – hibernate.hbm2ddl.auto is used by "pure" Hibernate, while the second one – spring.jpa.hibernate.ddl-auto is a Spring wrapper over the first one.
- This property instructs ORM on what to do with the database schema.
- There are five possible values for it:
1. create – first, Hibernate will drop the database tables mapped to the entities. Then, it will generate and execute a DDL to create a DB schema that complies with the JPA model.
2. create-drop – will do the same as the previous one, but Hibernate will drop the database tables mapped to the entities after the application shuts down.
3. update – Hibernate will generate DDL scripts only for new tables/columns in this mode. Even though the value is called update, it does not create scripts to change or drop existing columns. E.g., if you mark an attribute as unique or drop some from the entity code – Hibernate will ignore it.
4. validate – in this mode, Hibernate will not generate any DDL statements and won't touch your database. It will only check for full compliance of your JPA model with the database. In case of a mismatch, the application will fail to boot with a SchemaManagementException.
5. none – will do nothing.
- Indeed, all you need to know about the ddl-auto property is that it's not a good idea to use any of the above values except validate on the production stand.
- For testing, create/create-drop may be an OK choice.
- And if you don't want to re-fill the database every time while testing, you can use the update option.
- For better development experience, prefer specialized solutions to manage database changes like Liquibase or Flyway. Even simple .sql files written by hand or automatically generated by the JPA Buddy in conjunction with spring.sql.init.mode would do better because you:
1. have complete control over the DDL before its execution;
2. can set up proper Java to Database types mapping;
3. have no issues using the attribute converters and Hibernate types.

### 7. How to fetch data from the database using JPA?
- With JPA, there are several ways to fetch data from the database.
- Some of them are available out-of-the-box, and some require additional libraries. Let's have a look at them.
- We'll code the same thing for each approach to better see the difference. The assignment reads: "You have a PostgreSQL database with one table called "User".
Column name	Type \
id	        bigint \
first_name	varchar(50) \
last_name	  varchar(50) \
email	      varchar(255)
- Write a code to select all users whose email ends with 'gmail.com' and whose name is 'Alice'. Order the result by 'lastName'." \

a. *JPQL*
- This option is available out of the box and is probably the oldest way to fetch data.
- JPQL is a SQL-like query language created specifically for JPA.
- EntityManager is responsible for JPQL execution. Here is the task implementation:
```
entityManager.getTransaction().begin(); 

TypedQuery<User> query = entityManager.createQuery(  
        "SELECT u FROM User u " +  
        "where u.email like '%gmail.com' and u.firstName = ?1 " +  
        "order by u.lastName",  
        User.class)  
        .setParameter(1, "Alice");  

List<User> users = query.getResultList();  

entityManager.getTransaction().commit(); 
entityManager.close(); 
```
- Pros:
1. DB-agnostic queries;
2. No extra libraries needed.
- Cons:
1. No query validation at build time;
2. Limited capabilities compared to SQL.

b. *Criteria API*
- Criteria API introduces DSL (Domain Specific Language) to create queries.
- It allows us to write queries without SQL or JPQL, with Java and string references to entities' properties.
- As a result, we can build queries not from strings but Java objects.
- It adds some type-safety when we combine different predicates or add order by clause to the query.
- Still, a query can fail in runtime due to an entity property name typo.
- Below is the code for selecting all Alices registered on the gmail.com domain.
```
entityManager.getTransaction().begin();   

CriteriaBuilder cb = entityManager.getCriteriaBuilder();  
CriteriaQuery<User> cr = cb.createQuery(User.class);  
Root<User> root = cr.from(User.class);  

cr.select(root).where(  
        cb.and(  
                cb.like(root.get("email"), "%gmail.com"),  
                cb.equal(root.get("firstName"),
                cb.parameter(String.class, "name"))  
        )  
);  
cr.orderBy(cb.asc(root.get("lastName")));  

TypedQuery<User> query = entityManager.createQuery(cr);  
query.setParameter("name", "Alice");  

List<User> results = query.getResultList();  

entityManager.getTransaction().commit();  
entityManager.close();  
```
- Pros:
1. DB-agnostic queries;
2. No extra libraries needed;
--Type safety: we can pass parts of query as a parameter, concatenate them, etc. – fewer chances for typos.
- Cons:
1. No field names validation at build time;
2. The code is hard to read compared to SQL and JPQL.

c. *QueryDSL*
- QueryDSL is an external library that uses annotation processing to generate additional classes – called Q—types.
- These are copies of the JPA entities but introduce an API that allows us to create database queries.
- For example, if you have the User entity with firstName and lastName string attributes, then the generated Q-type will be called QUser and will have attributes with the same name but a different type - StringPath.
- Each attribute will have specific methods to compose queries.
- For example, like(), eq(), etc. Those methods form the DSL language that we can use.
- Let's have a look at the code example:
```
entityManager.getTransaction().begin();   

List<User> users = new JPAQuery<User>(entityManager)  
        .select(QUser.user)  
        .from(QUser.user)  
        .where(QUser.user.email.endsWith("gmail.com")  
                .and(QUser.user.firstName.eq("Alice")))  
        .orderBy(QUser.user.lastName.asc())  
        .fetch();  

entityManager.getTransaction().commit();  
entityManager.close();  
```
- Pros:
1. DB-agnostic queries;
2. Type safety;
3. Compile-time query validation.
- Con:
1. Require additional dependency;
2. Need to regenerate classes on data model change.

d.*Spring Data JPA @Query/Derived methods*
- Spring Data JPA is a part of the Spring Framework that allows us to use well-designed repositories API to execute database queries using derived method names or JPQL or SQL queries.
- Derived methods are repository interface methods named in a special way.
- They are very convenient for simple queries; sometimes, they may even be more powerful than JPQL queries.
- For example, there is no way to fetch top N records from the database using JPQL, although, with derived methods, you can complete this task easily.
- However, derived methods become hard to read and maintain for massive queries with many conditions.
- Let's have a look at the interface that can execute the query that we implemented earlier:
```
public interface UserRepository extends JpaRepository<User, Long> { 
     List<User> findByFirstNameAndEmailEndsWithOrderByLastNameAsc(String firstName, String email); 
}
```
- As we can see, the method name is barely readable. For such cases, we can use pure JPQL or even native SQL.
- Spring Data framework will do all the heavy lifting on substituting parameters, opening a transaction, etc.:
```
public interface UserRepository extends JpaRepository<User, Long> { 
    @Query("select u from User u " + 
           "where u.firstName = ?1 and u.email like concat('%', ?2) " + 
           "order by u.lastName") 
    List<User> findByNameAndEmail(String firstName, String email); 
}
```
- Additional bonus – method names and JPQL queries are verified at the application startup. It is not a compile-time check but much better than runtime failure.
- Pros:
1. No need to learn JPQL and SQL for simple queries;
2. Boot-time query validation;
3. The code is easy to read and use;
4. Adds some extra features like projections.
- Con:
1. Require Spring Data as a dependency;
2. Method names might be cumbersome for complex queries;
3. Native SQL queries are not checked at boot-time.

e. *Native Queries*
- Some SQL clauses are not supported in JPQL and hence in all other JPA-based DSL libraries.
- For these cases, we can use native SQL in JPA.
- It gives us some flexibility: we can use carefully optimized queries only when required and use JPA to avoid writing tons of simple SQL queries in other cases.
- Here is an example on how to execute SQL in JPA:
```
entityManager.getTransaction().begin();  
    Query users = (Query) entityManager.createNativeQuery( 
            """  
            SELECT u.id, u.first_name, u.last_name, u.email   
            FROM "user" u WHERE u.email like(CONCAT('%', :email)) and u.first_name= :firstName  
            ORDER BY u.last_name  
            """,  User.class) 
        .setParameter("email", "gmail.com") 
        .setParameter("firstName", "Alisa"); 
    List<User> authors = (List<User>) users.getResultList();
        entityManager.getTransaction().commit(); 
        entityManager.close(); 
```
And here's how it works in Spring Data JPA:
```
@Query(value = """ 
    SELECT u.id, u.first_name, u.last_name, u.email  
    FROM "user" u WHERE u.email like(CONCAT('%', :email)) and u.first_name= :firstName 
    ORDER BY u.last_name 
    """, nativeQuery = true) 
List<User> findByNameAndEmailNative(String firstName, String email); 
```
- Pros:
1. No limitations – we use pure SQL;
2. The code is easy to read and use;
3. Simpler to debug queries.
- Con:
1. Query correctness check only on execution;
2. Hard to refactor code on schema change;
3. Manual type cast – native queries cannot be properly parametrized.

### 8. What are the states of an entity in JPA?
JPA specifies four different object states:
1. *Transient* – All new entities have never been associated with an opened database session (Persistence Context) and do not have corresponding rows in the database yet;
2. *Managed* – All entities fetched from the database and associated with a Persistence Context. ORM tracks all the changes made to entities in this state. When we close the session without transaction rollback, ORM automatically submits all changes to the database;
3. *Detached* – Entities transit to this state when the database session is closed. The ORM no longer tracks any changes made to them. To save entities, we need to make them managed again by "attaching" them to the session. The simplest way is to invoke EntityManager's merge() method. Some frameworks (like Spring Data JPA) can do it automatically.
4. *Removed* – entities get into this state after we call the remove() method. They will only be removed from the database after we flush session changes or close it.

### 9. Why do we need equals()/hashCode(), and how to implement them correctly for JPA entities?
- By default, in Java, object instances are equal if their addresses in memory are equal.
- For JPA, this approach does not work well.
- If we fetch the same entity instance in different transactions, their addresses in memory will be different.
- It might cause problems with caching, issues with Set collections, etc.
- That's why it is essential to properly define the equals() method for JPA entities.
The same reasoning applies to the hashCode() method implementation.
- JDK collections framework and Hibernate-specific collections use this method heavily, so the improper implementation may affect application performance, lead to entities "loss" in collections, or even cause runtime exceptions if we use lazy attribute loading.
- There are some examples of such behavior in the article about Lombok in JPA.
- Naturally, entities are mutable. A database often generates even the id of an entity, so it gets changed after the entity is first persisted.
- This means there are no fields we can rely on to calculate the hash code value or use in entities equality computation.
- Let's see how we can do it. \
By implementing these methods, we should:
1. maintain decent performance;
2. consider the specifics of the JPA world;
3. save the contract between hashCode() and equals(). \
It looks like the following implementation looks like the most appropriate if we use Hibernate ORM:
```
@Override  
public boolean equals(Object o) {  
    if (this == o) return true;  
    if (o == null || Hibernate.getClass(this) != Hibernate.getClass(o))   
       return false;  
    User user = (User) o;  
    return id != null && Objects.equals(id, user.id);  
}  

@Override  
public int hashCode() {  
    return getClass().hashCode();  
}
``` 
- First, the hashCode() implementation always returns the same value.
- Even though such an approach is far from the best practices, this option is acceptable and preferable in the JPA world.
- The reason is simple: all fields, even id, may change when the entity moves from one state to another.
- So, if we don't want to lose an entity in the collection due to field value change, it's better to have one immutable value.
- Such an approach might sound terrible since it defeats the purpose of using multiple buckets in a HashSet or HashMap.
- However, for performance reasons, you should always limit the number of entities stored in a collection.
- It would be best if you never fetched thousands of entities to a Set because the performance penalty on the database side will affect your application much more than using a single hashed block.
- Accordingly, comparing hash codes in the equals() method makes no sense. The objects in our case will not be equal when:
1. the object or its id is null;
2. the ids of the objects do not match;
3. the objects belong to different classes.
- If the objects have the same references, we assume they are equal.
- Also, when the object IDs match and all checks above pass, we believe that the two objects are equal as well.

### 10. What does @Transactional annotation do? What are the ways to configure it?
- A database transaction is a sequence of actions treated as a single unit of work.
- In other words, either all actions will be executed or none.
- Spring provides a powerful mechanism for managing transactions.
- Simply annotating a method with @Transactional, we automatically open a database transaction when the method execution starts and close the transaction when it finishes. \

-----
The questions are: *what will happen if we call a transactional method from another one? Should we create a new transaction or reuse the same? If we open a new transaction, should it be able to read data changed in the calling method?*
- In fact, we can manage transactional methods behavior; let's see how we can do it.

*Transaction Propagation*
- Transaction propagation allows you to specify the behavior if a transactional method is executed when the transaction context already exists.
-  E.g., you can configure it to create a nested transaction inside an already existing one; or suspend an active transaction and create a new one. Here are all the available options:
1. REQUIRED – the default value. Spring uses the active transaction to execute the business logic. If no transaction exists, it creates a new one.
2. NESTED – If there's no active transaction, it works like REQUIRED. When there is an active transaction, Spring remembers a point where the method was called and creates a new transaction. In case of an execution error, the transaction will be rolled back to the saved point.
3. REQUIRES_NEW – Spring suspends the existing transaction if it exists and then creates a new one.
4. MANDATORY – If there is an active transaction, Spring uses it. Otherwise, it throws the TransactionRequiredException.
5. SUPPORTS – If there is an active transaction, Spring uses it. Otherwise, the code will be executed in the non-transactional form.
6. NOT_SUPPORTED – If there is an active transaction, Spring suspends it. Next, the code will be executed in the non-transactional form.
7,. NEVER – Spring throws TransactionalException if there is an active transaction. Otherwise, the code will be executed in the non-transactional form. \

*Transaction Isolation*
- Transaction isolation is one of the four ACID properties, along with atomicity, consistency, and durability.
- There are four isolation levels:
1. Read uncommitted;
2. Read committed;
3. Repeatable read;
4. Serializable.
- Each of them determines how users can interact with the data at the same time and what concurrency effects they may get.
- Spring fully supports all of them and provides another option – DEFAULT. In this mode, Spring will use the default isolation level of the database.
- So, for every transactional method, we can specify an isolation level hence managing changes visibility between transactions.

-- *@Transactional(readOnly = true)*
- If you only plan to get data from the database and not change it, consider setting the readOnly attribute to true.
```
@Transactional(readOnly = true) 
User findById(Integer id); 
```
- You can win some performance points by explicitly telling Spring that you only need to read the data.
- Also, depending on your database, Spring can omit table locks or even reject write operations you might trigger accidentally.

-- *@Modifying annotation*
- The @Modifying annotation is designed to be used along with the @Query annotation.
- When we use these two annotations together, we can perform not only SELECT statements but also INSERT, UPDATE and DELETE ones.
```
@Transactional 
@Modifying 
@Query("update User u set u.isActive = true where u.email is not null") 
int updateActivityStatus();
``` 

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

### 6.Explain how Spring Data REST handles pagination and sorting.
- Spring Data REST supports pagination and sorting by default. You can use query parameters like ?page=1&size=10&sort=name,asc in the URL to control pagination and sorting.

### 7.What is Pagination in Spring Data Rest,why do we need it and how to implement?
- Pagination in Spring Data REST refers to the process of dividing a large set of data into smaller, more manageable chunks or pages when querying data from a RESTful API.
- It allows clients to request and retrieve data in smaller portions rather than all at once, which is especially useful when dealing with large datasets.
- Pagination enhances the performance and usability of an API by reducing the amount of data transferred over the network and improving response times.
- Why We Need Pagination:
1. *Efficient Data Retrieval*: Pagination prevents the need to fetch and transfer the entire dataset in a single request, which can be time-consuming and resource-intensive.
2. *Reduced Network Load*: Smaller data payloads reduce the load on the network, improving response times and reducing the risk of timeouts or network congestion.
3. *Improved User Experience*: Users can navigate through large datasets more easily by requesting specific pages of data, making the application more user-friendly.
4. *Optimized Resource Usage*: Server and client resources are used more efficiently when only a portion of the dataset is retrieved.
- How to use :
a. let's assume you have a large set of products and you want to retrieve them page by page.
b. You can use the following endpoint to retrieve the first page of products (page 0, with 10 items per page):
```
GET /products?page=0&size=10
```
c. This request will return the first 10 products in the dataset. To retrieve subsequent pages, increment the page parameter:
```
GET /products?page=1&size=10
```

### 8.What is Sorting in Spring Data Rest,why do we need it and how to implement?
- Sorting is the process of arranging data in a specific order, typically in ascending (from smallest to largest) or descending (from largest to smallest) order, based on one or more criteria or attributes.
- Sorting is a fundamental operation in data processing and retrieval and is essential for organizing and presenting data in a meaningful way.
- Why We Need Sorting:
1. *Data Presentation*: Sorting allows data to be presented to users in a structured and easy-to-understand manner, making it more accessible and user-friendly.
2. *Search Efficiency*: Sorted data can be searched more efficiently using techniques like binary search, which significantly reduces the time complexity of retrieval operations.
3. *Data Analysis*: Sorting facilitates data analysis by organizing data in a way that patterns, trends, or outliers become more apparent.
4. *Report Generation*: For generating reports, invoices, or any document where data needs to be presented in a specific order, sorting is crucial.
5. *User Experience*: In user interfaces, sorted lists or tables provide a better user experience by helping users quickly find what they're looking for.
- For example, *?page=0&size=10&sort=name,asc* limits the result set to 10 items per page and sorts them by the name field in ascending order.
- How to use :
a. To sort products by price in ascending order, you can make a GET request to the endpoint with the sort parameter:
```
GET /products?sort=price
```
This request will return the products sorted by price from lowest to highest.
b. To sort in descending order, add the desc keyword to the sort parameter:
```
GET /products?sort=price,desc
```
This request will return the products sorted by price from highest to lowest.
c. Spring Data REST also supports sorting by multiple fields and custom sorting expressions. For example, to sort products first by price in ascending order and then by name in descending order:
```
GET /products?sort=price,name,desc
```
In your Spring Data REST application, the repository endpoints automatically handle sorting based on the query parameters provided in the request. You don't need to write explicit sorting code; it's built into the framework.

#### 9.What is the purpose of the @RepositoryRestResource annotation?
- The @RepositoryRestResource annotation allows you to customize the behavior of Spring Data REST for a specific repository. You can use it to configure paths, set exported flags, and more.
```
@RepositoryRestResource(path = "users")
public interface UserRepository extends CrudRepository<User, Long> {
}
```
-----
*For better understanding*

The *@RepositoryRestResource* annotation is a special annotation used in Spring Framework, particularly in Spring Data REST, to expose a Spring Data JPA repository as a RESTful web service. It's a way to make it easy to create a REST API for your data stored in a database. \

Here's a simplified explanation in layman's terms with a code example: \

Imagine you have a Java class representing an entity, like a Book, and you want to store information about books in a database. You also want to be able to retrieve, create, update, and delete books using a web API. \

1. *Without @RepositoryRestResource*:
Without using @RepositoryRestResource, you would typically have to write a lot of code to set up the endpoints, handle HTTP requests, and connect them to your database. This can be quite complex and time-consuming. \
```
// You'd have to create a controller like this
@RestController
@RequestMapping("/books")
public class BookController {
    // Implement methods to handle GET, POST, PUT, DELETE requests
    // Connect to the database, handle exceptions, etc.
}
```
You'd also have to write a service class to handle business logic and a repository class to interact with the database.

2. *With @RepositoryRestResource*:
When you use @RepositoryRestResource to expose a Spring Data JPA repository as a RESTful web service, you typically don't need to write a separate controller or service class for basic CRUD (Create, Read, Update, Delete) operations. The @RepositoryRestResource annotation takes care of automatically generating REST endpoints for your entity.
```
@Entity
public class Book {
    // Define fields, getters, setters, etc.
}
```
```
public interface BookRepository extends JpaRepository<Book, Long> {
    // Spring Data JPA automatically provides basic CRUD operations
}
```
Now, by simply adding @RepositoryRestResource to your repository interface like this:
```
@RepositoryRestResource(path = "books")
public interface BookRepository extends JpaRepository<Book, Long> {
}
```

- GET /books: Retrieve all books.
- POST /books: Create a new book.
- GET /books/{id}: Retrieve a specific book by ID.
- PUT /books/{id}: Update a specific book by ID.
- DELETE /books/{id}: Delete a specific book by ID.
So, in summary, @RepositoryRestResource simplifies the process of exposing your JPA repositories as RESTful APIs, saving you from writing a lot of boilerplate code. If you don't use it, you'll have to manually create controllers and handle HTTP requests and database interactions yourself.

-----
### 10.How can you customize the endpoints (URL paths) for Spring Data REST repositories?
- You can customize the endpoints by using the @RepositoryRestResource annotation's path attribute, as shown in the previous example.
- This will change the URL path to /users instead of the default.

### 11.Explain the concept of projection in Spring Data REST.
- In Spring Data REST, the concept of "projection" refers to the ability to shape the data that is returned from a REST API endpoint.
- Projections allow you to specify which fields of an entity should be included or excluded in the response, and they can be particularly useful when dealing with complex domain models or when you want to optimize the payload size of API responses.
```
@Projection(name = "userProjection", types = User.class)
public interface UserProjection {
    String getName();
    String getEmail();
}
```

-----
*To illustrate the concept of projection, here's a simple example using Spring Data REST*:
- Suppose you have an entity class Book with fields like id, title, author, publishedDate, and genre. You want to create a projection that only includes the title and author fields when fetching books:

```
@Projection(name = "titleAuthor", types = { Book.class })
public interface TitleAuthorProjection {
    String getTitle();
    String getAuthor();
}
```
In this example, we've defined a projection called TitleAuthorProjection that specifies only two fields (title and author) from the Book entity. \
Now, when you request the /books endpoint, you can specify the projection using a query parameter like ?projection=titleAuthor, and the response will only include the selected fields: 
```
GET /books?projection=titleAuthor
```

-----

### 12.How can you restrict the HTTP methods allowed on a Spring Data REST endpoint?
- You can restrict HTTP methods using the @RepositoryRestResource annotation's *collectionResourceRel* and *itemResourceRel* attributes along with the exported attribute to control which HTTP methods are allowed.
```
@RepositoryRestResource(
    collectionResourceRel = "users",
    itemResourceRel = "user",
    exported = false
)
public interface UserRepository extends CrudRepository<User, Long> {
}
```

-----
*For better understanding* \

In Spring Data REST, you can restrict the HTTP methods allowed on an endpoint using the @RepositoryRestResource annotation and its exported attribute. \
This allows you to control which HTTP methods (e.g., GET, POST, PUT, DELETE) are allowed for a particular repository endpoint. \

Let's explain this with a simple code example in layman's terms: \
Suppose you have a Spring Data JPA repository for a Book entity, and you want to restrict certain HTTP methods on the /books endpoint. \
You can do this using the @RepositoryRestResource annotation. \

Here's how you can restrict methods in code: 
```
@RepositoryRestResource(path = "books")
public interface BookRepository extends JpaRepository<Book, Long> {

    // By default, all CRUD methods are "exported," meaning they are allowed.
    // You can restrict specific methods using the `exported` attribute.

    @RestResource(exported = false) // This restricts the method.
    Book save(Book book);

    // Other repository methods...
}
```
In this example:
- We have a BookRepository interface that extends JpaRepository. By default, all CRUD methods like save, findById, findAll, delete, etc., are considered "exported," which means they are allowed to be accessed via HTTP.
- To restrict a specific method, such as save, from being accessible via HTTP, we use the @RestResource annotation on that method and set its exported attribute to false. This tells Spring Data REST not to expose the save method through HTTP. \

So, with this configuration:

- GET /books (Retrieve all books) is allowed by default.
- GET /books/{id} (Retrieve a specific book by ID) is allowed by default.
- DELETE /books/{id} (Delete a specific book by ID) is allowed by default. \
But:
- POST /books (Create a new book) is allowed by default.
- PUT /books/{id} (Update a specific book by ID) is allowed by default.
- POST /books/{id} (Update a specific book by ID) is allowed by default because it maps to the save method. \

By setting @RestResource(exported = false) on the save method, we have restricted the creation and updating of books via HTTP. Clients can still create and update books programmatically by calling the save method within your application, but they won't be able to do so via HTTP requests.

-----

### 13.What is the purpose of event handlers in Spring Data REST, and how can you define them?
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

### 14.Explain how to perform custom validation in Spring Data REST.
- Custom validation in Spring Data REST allows you to add your own validation logic to ensure that data meets specific criteria before it's persisted in your database.
- This is useful for enforcing business rules or data integrity constraints in your RESTful API.
- Let's break down custom validation with a code example in layman's terms and discuss what happens if you use it versus if you don't.
- Custom Validation Example:
Suppose you have a Book entity with a title field, and you want to ensure that every book title must start with a capital letter. You want to add custom validation to enforce this rule. \

*If you use custom validation*: \
First, you create a *custom validation annotation, say @TitleCase*, to mark fields that need to follow the capitalization rule:
```
@Target({ ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER })
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = TitleCaseValidator.class)
public @interface TitleCase {
    String message() default "Title must start with a capital letter";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```
Then, you implement the *TitleCaseValidator class*, which defines the validation logic:
```
public class TitleCaseValidator implements ConstraintValidator<TitleCase, String> {
    @Override
    public void initialize(TitleCase constraintAnnotation) {
    }

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        // Your custom validation logic here: Check if the title starts with a capital letter.
        return Character.isUpperCase(value.charAt(0));
    }
}
```
You apply the @TitleCase annotation to the title field of your Book entity:
```
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @TitleCase // Custom validation annotation
    private String title;

    // Other fields, getters, setters, etc.
}
```
Now, when you create or update a book via your Spring Data REST API, the custom validation will be applied automatically. \
If the title doesn't start with a capital letter, the validation will fail, and the operation will be rejected. \

*If you don't use custom validation*: \
Without custom validation, there would be no automatic check for the capitalization rule, and any value could be saved as the book title. \
This could lead to inconsistent or incorrect data in your database, and you might need to handle these validation checks manually in your application code, which can be error-prone and less maintainable. \

- In summary, custom validation in Spring Data REST allows you to enforce specific rules or constraints on your data before it's stored in the database.
- It helps maintain data integrity and consistency in your API. If you don't use custom validation, you would need to rely on manual validation in your application code, which can be less reliable and harder to manage.

### 16.How do you secure Spring Data REST endpoints?
- Securing Spring Data REST endpoints is crucial to protect your data and restrict access to authorized users or roles.
- You can use various security mechanisms to achieve this, such as Spring Security, to ensure that only authenticated and authorized users can perform operations on your RESTful API.
- Why Securing Spring Data REST Endpoints is Needed:
1. *Data Protection*: You want to prevent unauthorized access to sensitive data. Without security, anyone could read, modify, or delete your data, potentially exposing sensitive information.
2. *Data Integrity*: Security helps ensure that only valid and authorized changes are made to your data. Unauthorized modifications or deletions can lead to data corruption.
3. *Compliance*: Many applications need to adhere to security and privacy regulations (e.g., GDPR, HIPAA). Implementing security measures is essential to meet these requirements.

### 17.What is a custom search method in Spring Data REST, and how do you define one?
- A custom search method in Spring Data REST allows you to define your own search criteria and expose it as an HTTP endpoint in your RESTful API.
- This is useful when you need to perform complex searches on your data that go beyond simple CRUD operations.
- Custom search methods give you the flexibility to query your data based on specific requirements.
  
```
public interface UserRepository extends CrudRepository<User, Long> {
    List<User> findByLastName(String lastName);
}
```
-----

*Step 1: Define the Repository Interface* \

First, create a repository interface for your entity, extending JpaRepository or a similar Spring Data repository interface. \
In this example, we'll assume you have an entity called Book: \
```
@RepositoryRestResource(path = "books")
public interface BookRepository extends JpaRepository<Book, Long> {

    // Define custom search methods here

}
```
*Step 2: Define the Custom Search Method* \

Define a custom search method within your repository interface. \
You can use the @Query annotation to specify the JPQL (Java Persistence Query Language) query for your custom search. \
JPQL is a query language similar to SQL but used for querying JPA (Java Persistence API) entities.
```
@RepositoryRestResource(path = "books")
public interface BookRepository extends JpaRepository<Book, Long> {

    @Query("SELECT b FROM Book b WHERE b.author = :authorName")
    List<Book> findByAuthor(@Param("authorName") String authorName);

}
```

In this example, we've defined a custom search method findByAuthor that retrieves a list of books by a specific author's name. \
It uses the @Query annotation to specify the JPQL query. :authorName is a parameter that will be replaced with the value passed to the method. \

*Step 3: Use the Custom Search Method* \

Once you've defined the custom search method, you can use it in your REST API. \
When you send an HTTP request to the endpoint associated with the custom search, it will execute the custom query and return the results. \

For example, to search for books by a specific author's name, you can make a GET request to: \
```
GET /books/search/findByAuthor?authorName=John Doe
```
The findByAuthor part of the URL corresponds to your custom search method, and authorName=John Doe is a query parameter that you can use to filter the results.

-----


### 4.What is Spring boot Rest Controller?how is it beneficial?
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

**Annotations and Annotation related**

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
6. *
- The PATCH method is used to partially update a resource on the server. For example, if you want to update only some fields of an existing user, you can use a PATCH request to /users/{id} with the modified user data in the request body. In Spring Boot, you can use the @PatchMapping annotation to map a method to a PATCH request.
```
@PatchMapping("/users/{id}")
  public User patchUser(@PathVariable Long id, @RequestBody User user) {
    return userService.patchUser(id, user);
  }
```

**Questions as per dependency added in project**

### Q.Why is Jackson dependency used in Spring boot?important jackson dependencies?
- Jackson is one of the most used libraries of spring boot which translates JSON data to a Java POJO by itself and vice-versa. JSON stands for JavaScript-object-Notation and POJO is our plain-old-java-object class. 
- important jackson dependencies :
1. *jackson-databind* : General data-binding functionality for Jackson: works on core streaming API.
2. *jackson-core*: Core Jackson processing abstractions (aka Streaming API), implementation for JSON.
3. *jackson-annotations*: This library includes annotations like @JsonProperty, @JsonFormat, and others that you can use to customize the JSON mapping behavior.

