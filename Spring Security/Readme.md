### 1. What is Spring Security?
- Spring Security is a robust, custom-built authentication and access-controlled framework. It is the main standard for securing Spring-based applications.
- Spring Security framework focuses on providing secure authentication and authorization access to Java applications.
- Along with authentication and authorization, Spring Security helps us protect our projects from many common attacks.
- The major advantage of Spring Security is its customizability.

### 2. What are the core features of Spring Security?
The core features of Spring Security are:
- Extensive authentication and authorization support.
- Efficient detection and prevention of attacks like cross-site request forgery, session fixation, and clickjacking.
- Seamless Integration with Servlet API.
- Integration with Spring Web MVC (Model-View-Controller) features.

### 3. What are authentication and authorization in Spring Security?
1. *Authentication*:
- Authentication is the process of verifying the identity of a person or entity trying to access a particular resource.
- This is usually done by prompting the user to enter a username and password, and then checking to see if they match the credentials stored in a database.
- Once the user has been authenticated, they may be granted access to the resource in question, provided they have the necessary authorization.
- There are many different methods of authentication, including biometric authentication, token-based authentication, and multi-factor authentication.
2. *Authorization*:
- Authorization is the process of granting a user or entity access to a particular resource or data.
- This is usually done by verifying that the user has the necessary permissions or privileges to access the resource in question.
- In Spring Security, authorization is used to control access to web requests, methods, and individual domains.
- This ensures that users are only able to access the parts of a resource that they are supposed to and prevents unauthorized access.

### 4. What do you mean by session management in Spring Security?
- As far as security is concerned, session management relates to securing and managing multiple users' sessions against their request.
- It facilitates secure interactions between a user and a service/application and pertains to a sequence of requests and responses associated with a particular user.
- Session Management is one of the most critical aspects of Spring security as if sessions are not managed properly, the security of data will suffer.
- To control HTTP sessions, Spring security uses the following options: 
1. SessionManagementFilter.
2. SessionAuthneticationStrategy
- With these two, spring-security can manage the following security session options:   
- Session timeouts (amount of time a user can remain inactive on a website before the site ends the session.)
- Concurrent sessions (the number of sessions that an authenticated user can have open at once).
- Session-fixation (an attack that permits an attacker to hijack a valid user session).

### 5. Explain SecurityContext and SecurityContext Holder in Spring security.
- There are two fundamental classes of Spring Security: SecurityContext and SecurityContextHolder.  
1. *SecurityContext*: In this, information/data about the currently authenticated user (also known as the principal) is stored.So, in order to obtain a username or any other information about the user, you must first obtain the SecurityContext.
2. *SecurityContextHolder*: Retrieving the currently authenticated principal is easiest via a static call to the SecurityContextHolder. As a helper class, it provides access to the security context. By default, it uses a ThreadLocal object to store SecurityContext, so SecurityContext is always accessible to methods in the same thread of execution, even if SecurityContext isn't passed around.

### 6. What is Spring Security OAuth 2.0?
- OAuth 2.0 is an authorization protocol that enables client applications to access protected resources through an authorized server.
- A client application or a third party can gain limited access to an HTTP server on behalf of the resource owner or on its own behalf via OAuth 2.
- There are five key actors in OAuth 2.0:
1. User/resource owner: The person who owns the resource.
2. User-Agent: The browser used by the user.
3. Client: The application that requests an access token and is granted access after authorization. It means that the client passes credentials and its identification to the authorization server. It then uses the access token to access the resource server.
4. Authorization server: It issues access tokens to the client after successful authentication via the resource owner and obtaining authorization. In other words, the authorization server acts as a gatekeeper, ensuring that only properly authenticated and authorized clients are granted access to the protected resources.
5. Resource server: It provides access to requested resources after validating access tokens. If the access token is valid, the resource server will allow the client to access the resource. If the access token is invalid or has expired, the resource server will deny the client’s request and return an error message.

### 7. What is method security and why do we need it?
- Simply put, Spring method security lets us add or support authorization at the method level.
- Spring security checks the authorization of the logged-in user in addition to authentication.
- Upon login, the ROLE of the user is used to determine which user is authorized to access the resource.
- When creating a new user in WebSecurityConfig, we can specify his ROLE as well.
- A security measure applied to a method prevents unauthorized users and only allows authentic users.
- The purpose of method level security is not to facilitate users who have access but to prevent unauthorized users from performing activities beyond their privileges and roles. 
- Method level security is implemented using AOP (Aspect-Oriented Programming).

### 8. What is hashing in Spring Security?
- A hash function is a mathematical algorithm that takes in a string (such as a password) and produces a fixed-size output, known as a hash or hash value.
- One common example of a hash function is SHA-256, which is often used in cryptography to secure data.
- In the context of Spring Security, a hash function takes a password string as input and returns its hash, which is then stored in the database.
- Hashing adds a robust security layer to passwords and helps ward off malicious attacks by hackers.
- Any attempt to query the plain text from the hashed value by an attacker is considered computationally infeasible.
  
  ![alt text](https://www.educative.io/api/page/6568579261792256/image/download/6486269837443072?page_type=collection_lesson)

### 9. What is digest authentication?
- We can authenticate some web services like RESTful in several ways. However, advanced authentication methods require digestion.
- Digest authentication resolves several pitfalls of basic authentication by ensuring credentials are never sent in plain text across the wire.
- This involves applying a hash function to a username, password, and URI (Uniform Resource Identifier) to encode the credentials sent.
- It generates more complex cryptographic results by using the hashing technique, which is cryptographically secured.

### 7. What is the security filter chain in Spring Security?
- Spring Security implements the majority of its security features via the filter chain driven through standard servlet filters in web applications.
- A servlet filter intercepts requests before they arrive at the destination, which is a protected resource like a Spring controller.
- Subsequently, every request for a protected resource is eventually processed via the Spring Security filter chain to complete authentication and authorization procedures.

### 10. What is JWT?
- JSON Web Token (JWT) is an open standard RFC 7519 that defines a compact and independent method for securely sending trusted information and data among parties as a JSON object.
- This information is verifiable and trustworthy because it has a digital signature.
- We can sign JWTs using a secret or a public/private key pair using RSA or ECDSA, which are asymmetric algorithms.

![alt text](https://www.educative.io/api/page/6568579261792256/image/download/6257930853941248?page_type=collection_lesson)

- JWTs are best used in the following scenarios:
1. *Authorization*: This is a popular choice for using a JWT. Once a user logs in, each successive request will include the JWT, permitting the user to access routes, services, and resources that are allowed with that specific token.
2. *Information exchange*: Because JWTs can be digitally signed, they are a great way of securely transmitting information between parties.

### 11. What are the prerequisites for Spring Security?
- It requires Java 8 or a higher runtime environment.
- No special configuration files are required if using EJB or Servlet Container.
- Also, Spring Security doesn’t require us to configure a Java Authentication and Authorization Service (JAAS) policy file.
- It allows you to copy your target artifact, such as JAR, WAR, or EAR, from one system to another and works immediately without delay.

### 12. What are the advantages of the Spring JDBC template?
- Spring simplifies database‌ access with the Spring JDBC Template.
- The Spring JDBC Template has the following advantages over the standard JDBC:
- It provides org.springramework.jdbc.core.jdbcTemplate class in JDBC package that allows automatic resource cleanup like releasing the database connections.
- It converts the standard JDBC SQL exceptions into runtime exceptions.
- This action allows developers to act swiftly in response to errors. The template also converts vendor-specific error messages into an understandable format.
- It allows us to translate the SQL result directly into an object or a list of objects by using the RowMapper or ResultSetExtractor interface.
- It provides methods to write the SQL queries directly, saving a lot of work.

### 13. What are some security annotations that can involve Spring Expression Language (SpEL)?
- Spring Security uses SpEL for expression support. Expressions are evaluated with a root object as part of the evaluation context.
- The following annotations that allow the expression attributes to use authorization checks:
1. *@PreAuthorize*: This annotation is used to specify a security constraint that must be satisfied before a method is invoked. The constraint is specified as an expression that is evaluated against the security context.
2. *@PostAuthorize*: This annotation is similar to @PreAuthorize, but the expression is evaluated after the method has been invoked.
3. *@PreFilter*: We use this annotation to specify a security constraint that must be satisfied before a list of elements is processed. The constraint is specified as an expression that is evaluated against each element in the list.
4. *@PostFilter*: This annotation is the opposite of @PreFilter because the expression is evaluated after the list has been processed.
5. *@Secured*: This annotation is used to specify a list of security roles that are allowed to access a method or class. The roles are specified as strings, and the user must have at least one of the specified roles to be granted access.

### 14. Explain what is AuthenticationManager in Spring security.
- A Spring Security component called AuthenticationManager tells "How authentication will happen".
- Because the how part of this question depends on which authentication provider we are using for our application, an AuthenticationManager contains references to all the AuthenticationProviders.
- AuthenticationManager is the strategy interface for authentication, which has only one method: 
```
public interface AuthenticationManager  { 
    Authentication authenticate(Authentication authentication) 
    throws AuthenticationException; 
}
```
- AuthenticationManagers can perform one of three actions in their authenticate() method: 
1. If it can verify that the input represents a valid principal, it will return an Authentication (normally authenticated=true).
2. If the input is believed to represent an invalid principal, it will throw an AuthenticationException.
3. If it is unable to decide, it will return null.

### 15. What are some important filter classes for Spring Security?
- The Spring Security framework provides several filters that can be used to secure web applications. Some important filter classes include:
1. *UsernamePasswordAuthenticationFilter*: This filter is used to authenticate a user using a username and password.
2. *BasicAuthenticationFilter*: This filter is used to authenticate a user using basic authentication.
3. *SessionManagementFilter*: We use this to manage user sessions and prevent session hijacking.
4. *SecurityContextPersistenceFilter*: This filter is used to store the security context of a user across multiple requests.
5. *ExceptionTranslationFilter*: This filter is used to handle exceptions thrown during the security process and convert them into HTTP responses.
6. *FilterSecurityInterceptor*: This filter is used to enforce security constraints on HTTP requests based on the configured security rules.
These are just a handful of the filters available in Spring Security. It is imperative that you choose the appropriate filters for your application based on your security needs.

