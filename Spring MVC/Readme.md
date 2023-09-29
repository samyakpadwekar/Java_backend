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
### 3.What is Model 2 architecture?
### 4.What is Model 2 Front Controller architecture?
### 5.What is Dispatcher Servlet(Front COntroller)?
### 6.How do you set up Dispatcher Servlet?
### 7.How to Get Servletcontext and Servletconfig Objects in a Spring Bean?
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

### 8.What Is a Controller in Spring Mvc?
- Controllers control the flow of the application execution.
- In Spring MVC architecture the DispatcherServlet works as Front Controller.
- DispatcherServlet process the request and pass the request to the controller class annotated with @Controller.
- Each controller class is responsible to handle one or more requests of a certain type.

### 9.What is a RequestMapping?

### 10.How Does the @Requestmapping Annotation Work?
- The @RequestMapping is used to map web request to the controller in Spring MVC application. We can apply the @RequestMapping annotation to class-level and/or method-level in a controller.


### 11.Can you show an example controller method in Spring MVC?

### 12.What is Model?
### 13.What is ModelAndView?
### 14.What is a ViewResolver?

### 15.What is a form backing object?
### 16.How is validation done using Spring MVC?
### 17.What is BindingResult?
### 18.How do you map validation results to your view?
### 19.What are Spring Form Tags?
### 20.What is a Path Variable?
### 21.What is a Model Attribute?
### 22.What is a Session Attribute?
### 23.What is a init binder?
### 24.How do you set default date format with Spring?
### Why is Spring MVC so popular?
