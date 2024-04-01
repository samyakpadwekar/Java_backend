### 1. What is Spring Boot?
- Spring Boot is an open-source framework designed to simplify the setup, configuration, and development of production-ready Spring applications.
- It takes away much of the boilerplate code and configuration required in traditional Spring applications, allowing developers to focus on writing business logic.

### 2. What are the important Goals of Spring Boot?
The key goals of Spring Boot are:
- To provide a quick and efficient way to create standalone, production-ready Spring applications.
- To eliminate the need for extensive configuration by using sensible defaults.
- To enable a microservices-based architecture with built-in support for embedded servers and cloud integration.

### 3. What are the important Features of Spring Boot?
Some essential features of Spring Boot include:
1. *Auto Configuration*: Automatically configures common components based on project dependencies. ex. @EnableAutoConfiguration or @SpringBootApplication annotated class.
2. *Starter Projects*: Pre-configured templates for various types of applications.(starter dependencies)
3. *Embedded Servers*: Support for embedding web servers like Tomcat or Jetty.
4. *Spring Boot Actuator*: Built-in tools for monitoring and managing applications.
5. *Spring Initializr*: A web-based tool for generating Spring Boot projects.
6. *Externalized Configuration*: Easy management of application properties.

### 4. Compare Spring Boot vs Spring?
1. *Configuration*: 
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
        ApplicationContext context
            = new AnnotationConfigApplicationContext(
                CollegeConfig.class);
 
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

3. Embedded Server: \
a. Spring:
In traditional Spring applications, you need to deploy your application to an external web server like Tomcat, Jetty, or WildFly. \
b. Spring Boot:
Spring Boot includes an embedded web server (e.g., Tomcat, Jetty, or Undertow) by default, making your application self-contained and reducing the need for external server deployment.

4. Configuration Properties: \
a. Spring:
In Spring, you manage configuration properties through XML or @PropertySource annotations. \
b. Spring Boot:
Spring Boot simplifies property configuration by providing application.properties or application.yml files. You can easily define properties and override them based on profiles or external configuration.

5. Auto-Configuration: \
a. Spring:
In Spring, you need to configure many components manually, such as data sources, security, and view resolvers. \
b. Spring Boot:
Spring Boot's auto-configuration feature automatically configures many common components based on the dependencies you include in your project. For example, adding spring-boot-starter-data-jpa automatically configures a data source and entity manager.

6. Convention Over Configuration: \
a. Spring:
Spring follows the principle of "explicit configuration," where you need to provide explicit configuration details for most components. \
b. Spring Boot:
Spring Boot follows the principle of "convention over configuration." It provides sensible defaults, making it easy to get started without extensive configuration.

7. Application Entry Point: \
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
