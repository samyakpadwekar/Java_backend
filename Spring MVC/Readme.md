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

### 1.How to Get Servletcontext and Servletconfig Objects in a Spring Bean?
### 2.What Is a Controller in Spring Mvc?
### 3.How Does the @Requestmapping Annotation Work?
### 4.What is Model 1 architecture?
### 5.What is Model 2 architecture?
### 6.What is Model 2 Front Controller architecture?
### 7.Can you show an example controller method in Spring MVC?
### 8.Can you explain a simple flow in Spring MVC?
### 9.What is a ViewResolver?
### 10.What is Model?
### 11.What is ModelAndView?
### 12.What is a RequestMapping?
### 13.What is Dispatcher Servlet?
### 14.How do you set up Dispatcher Servlet?
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
