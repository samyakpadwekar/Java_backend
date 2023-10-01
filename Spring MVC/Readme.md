Spring MVC Framework follows the Model-View-Controller design pattern. It is used to develop web applications. It works around DispatcherServlet. DispatcherServlet handles all the HTTP requests and responses. It dispatches the requests to handlers. It uses @Controller and @RequestMapping as default request handlers. The @Controller annotation defines that a particular class is a controller. @RequestMapping annotation maps web requests to Spring Controller methods. The terms model, view, and controller are as follows: 
1. Model: The Model encapsulates the application data.
2. View: View renders the model data and also generates HTML output that the client’s browser can interpret.
3. Controller: The Controller processes the user requests and passes them to the view for rendering.

Spring MVC Framework works as follows:
- All the incoming requests are intercepted by the DispatcherServlet that works as the front controller.
- The DispatcherServlet then gets an entry of handler mapping from the XML file and forwards the request to the controller.
- The object of ModelAndView is returned by the controller.
- The DispatcherServlet checks the entry of the view resolver in the XML file and invokes the appropriate view component.

Advantages of Spring MVC Framework
1. The container is used for the development and deployment of applications and uses a lightweight servlet.
2. It enables rapid and parallel development.
3. Development of the application becomes fast.
4. Easy for multiple developers to work together.
5. Easier to Update the application.
6. It is Easier to Debug because we have multiple levels in the application.

Disadvantages of Spring MVC Framework
1. It has high complexity to develop the applications using this pattern.
2. It is not suitable for small applications which affect the application’s performance and design.

### 1.Explain a simple flow in Spring MVC?
![alt text](https://terasolunaorg.github.io/guideline/1.0.1.RELEASE/en/_images/RequestLifecycle.png)

1. Client requests for a page by specifying the Web URL for the page.Client request is intercepted by the *Dispatcher Servlet(Front Controller)*. *Dispatcher Servlet* is a servlet specified in Web.XML file (for XML Based configurations) or in the Web Configuration class (for java based configurations).
2. Dispatcher Servlet uses *Handler Mapping* to find out the relevant controller class to which request should be passed for subsequent processing.*Handler Mapping* returns the (selected Handler) and *Controller* to *DispatcherServlet*.
3. *DispatcherServlet* dispatches the task of executing of business logic of *Controller* to *HandlerAdapter*.
4. *HandlerAdapter* calls the business logic process of *Controller*.
5. *Controller* class will also be responsible for returning the *ModelAndView* object back to the *Dispatcher Servlet* after getting all business logic executed. *ModelAndView* object returned by the *Controller* back to the *Dispatcher Servlet* specifies both view and model objects.
6. After receiving *ModelAndView* object from the *Controller*, *Dispatcher Servlet* now sends model object to *View Resolver* to get the name of the view which needs to be rendered.*ViewResolver* returns the *View* mapped to View name.
7. Once the view to be rendered has been identified, Dispatcher Servlet passes model object to the *View*. Model object contains the data which needs to be displayed in the view.
8. *View* renders Model data and returns the response.This view is returned to the client and client can see the view and associated data on his browser. Views can be designed in any front-end technology.

### 2.What is Model 1 architecture?
- Early web application design regarded the *JSP page* as the focal point for the entire application.
- Termed Model 1 architecture, the JSP page not only contains the display elements to output HTML, but is also responsible for extracting HTTP request parameters, call the business logic (implemented in JavaBeans, if not directly in the JSP), and handle the HTTP session.
- Although Model 1 is suitable for simple applications, this architecture usually leads to a significant amount of scriptlets (Java code embedded within HTML code in the JSP page), especially if there is a significant amount of request processing to be performed. \
The following diagram illustrates the JSP Model 1 architecture.
![alt text](https://download.oracle.com/otn_hosted_doc/jdeveloper/1012/developing_mvc_applications/images/struts_model1.gif)

### 3.What is Model 2 architecture?
- As a response to the Model 1 architecture, Apache Software Organization developed the Jakarta Project's Struts framework. The MVC Model 2 paradigm applied to web applications lets you separate display code (for example, HTML and tag libraries) from flow control logic (Struts action classes).
- The following figure illustrates the Model 2 web application architecture, where Servlets control the flow of the web application and delegate the business logic to external components, usually JavaBeans or EJBs, while JSP pages generate the HTML for web browsers:

![alt text](https://download.oracle.com/otn_hosted_doc/jdeveloper/1012/developing_mvc_applications/images/struts_model2.gif)

The following information gives a brief overview of the MVC Model 2 design pattern:
- The Model portion of an MVC-based system typically comprises JavaBean classes that define the internal state of the system; they also specify the actions that can be taken to change that state.
- The View portion is constructed using JSP technology. JSP pages can contain static HTML (or XML) text called "template text", plus the ability to insert dynamic content based on the interpretation (at page request time) of special action tags. The JSP environment includes a set of custom JSP tag libraries (such as the Struts tag libraries), standard JSP action tags (such as those described in the JavaServer Pages Specification), and a facility to install your own JSP custom tag libraries.
- The Controller portion of the application is focused on receiving requests from the client (typically a user running a web browser), deciding what business logic function is to be performed, and then delegating responsibility for producing the next phase of the user interface to an appropriate View component. In Struts, the primary components of the Controller is a servlet of class ActionServlet and the class RequestProcessor.

### 4.What is Model 2 Front Controller architecture?
- Front Controller class diagram
  
![alt text](https://www.oracle.com/img/tech/figure07-07.jpg)

- Front Controller Sequence Diagram

![alt text](https://www.oracle.com/img/tech/figure07-08.jpg)

- *Controller* : The controller is the initial contact point for handling all requests in the system. The controller may delegate to a helper to complete authentication and authorization of a user or to initiate contact retrieval.
- *View* : A view represents and displays information to the client. The view retrieves information from a model. Helpers support views by encapsulating and adapting the underlying data model for use in the display.
- *Dispatcher* : A dispatcher is responsible for view management and navigation, managing the choice of the next view to present to the user, and providing the mechanism for vectoring control to this resource.
- Helper* : A helper is responsible for helping a view or controller complete its processing. Thus, helpers have numerous responsibilities, including gathering data required by the view and storing this intermediate model, in which case the helper is sometimes referred to as a value bean.
- 
### 5.What is Dispatcher Servlet(Front COntroller)?
> DispatcherServlet handles an incoming HttpRequest, delegates the request, and processes that request according to the configured HandlerAdapter interfaces that have been implemented within the Spring application along with accompanying annotations specifying handlers, controller endpoints, and response objects.
- DispatcherServlet acts as the Front Controller for Spring-based web applications.
- Any request is going to come into our website the front controller is going to stand in front and is going to accept all the requests and once the front controller accepts that request then this is the job of the front controller that it will make a decision that who is the right controller to handle that request.
- For example, refer to the below image.

![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20220302055243/DispatcherServlet.jpg)

- Suppose we have a website called student.com and the client is make a request to save student data by hitting the following URL student.com/save and its first come to the front controller and once the front controller accepts that request it is going to assign to the Controller_1 as this controller handle the request for /save operation. Then it is going to return back the response to the Client. 
- The front controller is already created by the Spring Framework Developer, and the name of that particular controller is *DispatcherServlet*. You can use that front controller in your Spring MVC project. You really not required to create a front controller but you can reuse that front controller created by the Spring Framework Developer and they named it as DispatcherServlet.

### 6.How do you set up Dispatcher Servlet?
- In Spring MVC project,go to *src > main > webapp > WEB-INF > web.xml* file and here we have to configure our front controller inside a *<servlet>…</servlet>* tag something like this. 
```
<servlet>
      <!-- Provide a Servlet Name -->
    <servlet-name>frontcontroller-dispatcher</servlet-name>
    <!-- Provide a fully qualified path to the DispatcherServlet class -->
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
</servlet>
```
Now tell this servlet to handle all the requests coming to our website called student.com (for this example). So the way we are going to tell the above servlet is we can write something like this
```
<servlet-mapping>
      <!-- Provide a Servlet Name that you want to map -->
    <servlet-name>frontcontroller-dispatcher</servlet-name>
    <!-- Provide a url pattern -->
    <url-pattern>/student.com/*</url-pattern>
</servlet-mapping>
```
So this does mean that the servlet “frontcontroller-dispatcher” is going to handle all the requests starting from student.com/anything, that may be student.com/save or student.com/get, anything. But it must start with student.com. So we are done with creating a Dispatcher Servlet.

### 7.When Dispatcher Servlet will be Initialized? 
- The Dispatcher Servlet will be Initialized once we deploy the created dynamic web application inside the tomcat server. So before deploying it let’s add the following line inside the web.xml file 
```
<load-on-startup>1</load-on-startup>
```
So now the modified code for the servlet is 
```
<servlet>
      <!-- Provide a Servlet Name -->
    <servlet-name>frontcontroller-dispatcher</servlet-name>    
    <!-- Provide a fully qualified path to the DispatcherServlet class -->
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>
```
Why this line load-on-startup>1?
- This will make sure that whenever your server will get started the *DispatcherServlet* will get initialized. 
- And if you are not writing this line of code then whenever the first request will come to your server starting from /student.com at that time only the DispatcherServlet will be initialized and we don’t want it. 
- We want the DispatcherServlet will be initialized during the time of the server startup. That’s why we have written this line of code.

### 8.How to Get Servletcontext and Servletconfig Objects in a Spring Bean?
There are two options for getting ServletContext and ServletConfig in a Spring Bean.
- Use *@Autowired* annotation to inject ServletContext and ServletConfig in Spring Bean.
- Implement *Spring aware interfaces* in the class that depends on ServletConfigor ServletContext.
Using @Autowired annotation
```
@Autowired
ServletContext servletContext;
@Autowired
ServletConfig servletConfig;
```
Implementing Spring aware interfaces
```
public class ServletConfigAwareClass implements ServletConfigAware {

 private ServletConfig config;

 public void setServletConfig(ServletConfig servletConfig) {
  this.config = servletConfig;
 }
```

### 9.What Is a Controller in Spring Mvc?
- Controllers control the flow of the application execution.
- In Spring MVC architecture the DispatcherServlet works as Front Controller.
- DispatcherServlet process the request and pass the request to the controller class annotated with @Controller.
- Each controller class is responsible to handle one or more requests of a certain type.

### 10.What is a RequestMapping?
- *@RequestMapping* is one of the most widely used Spring MVC annotation.
- *org.springframework.web.bind.annotation.RequestMapping* annotation is used to map web requests onto specific handler classes and/or handler methods.
- @RequestMapping can be applied to the controller class as well as methods.

### 11.How Does the @Requestmapping Annotation Work?
- The @RequestMapping is used to map web request to the controller in Spring MVC application. We can apply the @RequestMapping annotation to class-level and/or method-level in a controller.
- When configuring Spring MVC, you need to specify the mappings between the requests and handler methods.
- The class-level annotation maps a specific request path or pattern onto a controller. You can then apply additional method-level annotations to make mappings more specific to handler methods. 

-----
- *@RequestMapping with Class*: We can use it with class definition to create the base URI. For example:
```
@Controller
@RequestMapping("/home")
public class HomeController {

}
```
Now /home is the URI for which this controller will be used. This concept is very similar to servlet context of a web application.

- *@RequestMapping with Method*: We can use it with method to provide the URI pattern for which handler method will be used. For example:
```
@RequestMapping(value="/method0")
@ResponseBody
public String method0(){
	return "method0";
}
```
Above annotation can also be written as @RequestMapping("/method0"). On a side note, I am using @ResponseBody to send the String response for this web request, this is done to keep the example simple. Like I always do, I will use these methods in Spring MVC application and test them with a simple program or script.

- *@RequestMapping with Multiple URI*: We can use a single method for handling multiple URIs, for example:
```
@RequestMapping(value={"/method1","/method1/second"})
@ResponseBody
public String method1(){
	return "method1";
}
```
If you will look at the source code of RequestMapping annotation, you will see that all of it’s variables are arrays. We can create String array for the URI mappings for the handler method.

- *@RequestMapping with HTTP Method*: Sometimes we want to perform different operations based on the HTTP method used, even though request URI remains same. We can use @RequestMapping method variable to narrow down the HTTP methods for which this method will be invoked. For example:
```
@RequestMapping(value="/method2", method=RequestMethod.POST)
@ResponseBody
public String method2(){
	return "method2";
}

@RequestMapping(value="/method3", method={RequestMethod.POST,RequestMethod.GET})
@ResponseBody
public String method3(){
	return "method3";
}
```

- @RequestMapping with Headers: We can specify the headers that should be present to invoke the handler method. For example:
```
@RequestMapping(value="/method4", headers="name=pankaj")
@ResponseBody
public String method4(){
	return "method4";
}
	
@RequestMapping(value="/method5", headers={"name=pankaj", "id=1"})
@ResponseBody
public String method5(){
	return "method5";
}
```
-----

### 12.What is @PathVariable & @RequestParam?
- @RequestParam and @PathVariable can both be used to extract values from the request URI, but they are a bit different.
- While @RequestParam extract values from the query string, @PathVariable extract values from the URI path.
- Like for @PathVariable, it will be
```
@GetMapping("/foos/{id}")
@ResponseBody
public String getFooById(@PathVariable String id) {
    return "ID: " + id;
}
```
Then we can map based on the path:
http://localhost:8080/spring-mvc-basics/foos/abc
ID: abc
- And for @RequestParam, it will be:
```
@GetMapping("/foos")
@ResponseBody
public String getFooByIdUsingQueryParam(@RequestParam String id) {
    return "ID: " + id;
}
```
which would give us the same response, just a different URI:
http://localhost:8080/spring-mvc-basics/foos?id=abc
ID: abc
- Both @RequestParam and @PathVariable can be optional.
- We can make *@PathVariable* optional by using the required attribute starting with Spring 4.3.3:
```
@GetMapping({"/myfoos/optional", "/myfoos/optional/{id}"})
@ResponseBody
public String getFooByOptionalId(@PathVariable(required = false) String id){
    return "ID: " + id;
}
```
Then we can do either:
http://localhost:8080/spring-mvc-basics/myfoos/optional/abc
ID: abc
or:
http://localhost:8080/spring-mvc-basics/myfoos/optional
ID: null
- For @RequestParam, we can also use the required attribute.
- Note that we should be careful when making @PathVariable optional, to avoid conflicts in paths.

### 13.Can you show an example controller method in Spring MVC along with dispatcher servlet? (for understanding)
- Let’s look at the deployment descriptor (web.xml) where we will configure DispatcherServlet servlet as the front controller.
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns="https://xmlns.jcp.org/xml/ns/javaee" 
 xsi:schemaLocation="https://xmlns.jcp.org/xml/ns/javaee https://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>Spring-Controller</display-name>
  <!-- Add Spring MVC DispatcherServlet as front controller -->
	<servlet>
        <servlet-name>spring</servlet-name>
        <servlet-class>
                org.springframework.web.servlet.DispatcherServlet
        </servlet-class>
        <init-param>
       		<param-name>contextConfigLocation</param-name>
       		<param-value>/WEB-INF/spring-servlet.xml</param-value>
    		</init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
 
    <servlet-mapping>
        <servlet-name>spring</servlet-name>
        <url-pattern>/</url-pattern> 
    </servlet-mapping>
</web-app>
```
-Finally, we have following spring context file. Here we are configuring our application to be annotation-based and providing root package for scanning spring components. We are also configuring InternalResourceViewResolver bean and providing details of view pages.
```
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="https://www.springframework.org/schema/mvc"
	xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:beans="https://www.springframework.org/schema/beans"
	xmlns:context="https://www.springframework.org/schema/context"
	xsi:schemaLocation="https://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd
		https://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
		https://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

	<!-- Enables the Spring MVC @Controller programming model -->
	<annotation-driven />

	<context:component-scan base-package="com.journaldev.spring" />

	<!-- Resolves views selected for rendering by @Controllers to JSP resources 
		in the /WEB-INF/views directory -->
	<beans:bean
		class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/" />
		<beans:property name="suffix" value=".jsp" />
	</beans:bean>

</beans:beans>
```
Our configuration XML files are ready, let’s move on to the Controller class now.
```
package com.journaldev.spring.controller;

import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

	@GetMapping("/hello")
	public String home(Locale locale, Model model) {
		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
		String formattedDate = dateFormat.format(date);
		model.addAttribute("serverTime", formattedDate);
		return "home";
	}

}
```
We have defined a single request handler method, it’s accepting GET requests with URI “/hello” and returning “home.jsp” page as the response. Notice that we are setting an attribute to the model, which will be used in the home.jsp page.

### 12.What is Model?
> Java-5-specific interface that defines a holder for model attributes. Primarily designed for adding attributes to the model. Allows for accessing the overall model as a java.util.Map.
- Model is an essential part of MVC pattern which is widely used in Spring.
- A Model is a holder of the context data passed by a Controller to be displayed on a View.
- You can use only one Model which contains more data distinct with a unique key because the Model is based on the java.util.Map 

### 13.What is ModelAndView?
- Holder for both Model and View in the web MVC framework. Note that these are entirely distinct.
- This class merely holds both to make it possible for a controller to return both model and view in a single return value.
- Represents a model and view returned by a handler, to be resolved by a DispatcherServlet.

### 14.What is a ViewResolver?
- The ViewResolver let SPring MVC application to render models in a browser without binding to a specific view technology (e.g. JSP or Thymeleaf).
- This works by providing a mapping between view names and actual views.
- View addresses the preparation of data before handing over to a specific view technology.

### 15.What is a form backing object?
- The client-side HTML page fields are mapped with back end Java bean class. This is called as Form Backing Bean Object.
- It is an object which will have the data of your form. It is automatically initialized so you don't have to get data from form and set it to object's fields.
- In servlets we need to get data as:
```
request.getParameter(String name);
```
then we have to initialize the respective field, but in spring this step is done by spring.

### 16.How to validate form data in Spring Web MVC?
- Spring provides built-in support to use JSR-303 based bean validation.
- For using JSR-303 based validation, we need to annotate bean variables with the required validations.
- Let’s take a simple example to validate customer object
```
import javax.validation.constraints.Min;
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;

public class Customer {

 @NotNull
 @Size(min = 2, max = 30)
 private String name;

 @NotNull
 @Min(18)
 private Integer age;

 //getter and setters

}
```
To trigger JSR-303 based validation, we only need to annotate our incoming object with a @Validannotation
```
@Controller
public class WebController {

 @PostMapping("/")
 public String checkPersonInfo(@Valid Customer customer, BindingResult bindingResult) {

  if (bindingResult.hasErrors()) {
   return "form";
  }

  return "redirect:/results";
 }
}
```
Spring validation also provides an interface that can create custom validators (in a case out of the box validator does not satisfy the requirements.)

### 17.What is BindingResult?
- BindingResult is an interface which dictates how the object that stores the result of validation should store and retrieve the result of the validation(errors, attempt to bind to disallowed fields etc).
>[BindingResult] is Spring’s object that holds the result of the validation and binding and contains errors that may have occurred. The BindingResult must come right after the model object that is validated or else Spring will fail to validate the object and throw an exception. \
> When Spring sees @Valid, it tries to find the validator for the object being validated. Spring automatically picks up validation annotations if you have “annotation-driven” enabled. Spring then invokes the validator and puts any errors in the BindingResult and adds the BindingResult to the view model.

### 18.How do you map validation results to your view?
### 19.What are Spring Form Tags?
- The ‘form‘ tag renders an HTML ‘form‘ tag.
- It exposes a binding path to inner tags for binding the data entered.
- It puts the command object in the PageContext so that the command object can be accessed by all the inner tags.
- All the other tags in the spring tag library are nested tags of this form tag.
- Below is an example of the form tag:
```
<form:form action="submit" method="post" modelAttribute="welcome">
```
This spring form’s form tag will generate the standard HTML form tag while processing like below,
```
<form id="welcome" action="submit" method="post">
```

### 22.What is a Session Attribute?
- @SessionAttributes is used to store model attributes in the HTTP Servlet session between requests.
- It is a type-level annotation that declares the session attributes used by a specific controller.
- This typically lists the names of model attributes or types of model attributes that should be transparently stored in the session for subsequent requests to access.
- The following example uses the @SessionAttributes annotation:
```
@Controller
@SessionAttributes("pet") 
public class EditPetForm {
	// ...
}
```
- On the first request, when a model attribute with the name, pet, is added to the model, it is automatically promoted to and saved in the HTTP Servlet session.
- It remains there until another controller method uses a SessionStatus method argument to clear the storage, as the following example shows:
```
@Controller
@SessionAttributes("pet") - 1
public class EditPetForm {

	// ...

	@PostMapping("/pets/{id}")
	public String handle(Pet pet, BindingResult errors, SessionStatus status) {
		if (errors.hasErrors) {
			// ...
		}
		status.setComplete(); - 2
		// ...
	}
}
```
1->Storing the Pet value in the Servlet session.
2->Clearing the Pet value from the Servlet session.

### 23.What is a init binder?
- The Init Binder is an annotation that is used to customize the request being sent to the controller.
- It helps to control and format requests that come to the controller as it is defined in the controller.
- Uses
1. Before, you had to resort to manually parsing the date:
```
 public void webmethod(@RequestParam("date") String strDate) {
    Date date = ... // manually parse the date
 }
```
Now you can get the parsed date directly:
```
 public void webmethod(@RequestParam("date") Date date) {
 }
```
2. If your jsp page supplies a date on the form yyyy-MM-dd you can retrieve it as a Date object directly in your controller.
3. Spring tries against all registered editors to see if values can be converted into objects. You don't have to do anything in the object itself, that's the beauty of it. 

### 24.What is Spring MVC Interceptor and how to use it?
- Interceptors are useful to intercept the client request and process it. There are three options to intercept client request using Spring interceptors.
1. preHandle
2. postHandle
3. afterComplete (after the view is rendered to the client)
- Interceptors are useful for cross-cutting concerns and help us avoid duplicate code (e.g. logging, profiling etc.).We can create spring interceptor by implementing a HandlerInterceptor interface or by extending the abstract class HandlerInterceptorAdapter.

### 24.How to handle exceptions in Spring MVC?
1. Spring MVC provides the following three options for exception handling
2. @ExceptionHandler Annotation – ExceptionHandler is a Spring annotation handle exceptions thrown by request handling. This annotation works at the @Controller level.
<em><strong>@ControllerAdvice</strong></em> Annotation – This annotation supports global Exception handler mechanism. A controller advice allows you to use exactly the same exception handling techniques but applies them across the application, not just to an individual controller.
3. HandlerExceptionResolver – Resolve any exception thrown by the application.

### 25.What is the difference between @Controller and @RestController?
- There are few differences between @Controller and @RestController annotation:
1. @Controller annotation marks a class as Spring MVC Controller while the @RestController is a convenience annotation which also adds both @Controller and @ResponseBody annotation together.
2. @RestController automatically converts the response to JSON/XML.
3. The @RestController annotation cannot return a view while @Controller can do that.
Here is a definition to both for better clarity:
```
@Controller
public class ControllerExample{

  @RequestMapping(value={"/uri"})
  @ResponseBody
  public CustomResponse method(){
      //return response
   }
}
```
```
@RestController
public class ControllerExample{

  @RequestMapping(value={"/uri"})
  public CustomResponse method(){
      //return response
   }
}
```
