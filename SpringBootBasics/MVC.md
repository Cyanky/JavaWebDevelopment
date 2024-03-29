MVC is an acronym that stands for Model-View-Controller, and it's a common software pattern for user interface design. Traditionally, it divides the roles of components in an app into three layers:

- the **Model**, which is responsible for maintaining the state of an application,
- the **View**, which is responsible for displaying the UI to the user,
- and the **Controller**, which is responsible for processing user actions (sent from the View) to update the Model, and for forwarding those updates back to the View

MVC is an abstract pattern, though, and every library implements it differently. Spring MVC is built around the browser as a platform, and it organizes these roles like this:

- **HTML templates** are the views - each one represents a specific screen or screen component that the user is shown.
- **Spring beans** are the controllers - specifically, Spring MVC gives an `@Controller` annotation that we can use to register our beans as controllers. Think of Spring bean controllers as specialized application components that can define methods to handle specific user requests. Those methods are responsible for choosing the HTML template that is generated in response, as well as for populating the `Model` object for that template.
- **`Model` objects** are the models - every controller method can take an optional `Model` argument, and by reading and changing the data inside of it, the controller can read user-submitted data and populate the template with the changes. Think of the Model class a simple data-transfer object: something that can store various bits of data with keys to look that data up, and that can be passed between the browser, the template engine, and the controller to facilitate the transfer of data between the user and the application.

In order to start using Spring MVC, we need two main elements: an HTML template to define the user interface, and a Spring MVC `@Controller`-annotated bean to serve that template and populate it with data.

In our example so far, our "template" is actually just a static HTML page that displays a greeting. The main takeaway about templates so far is to remember to place them in the right folder - `src/main/resources/templates` under the project root directory. When we choose a template in our controller, we do so by specifying the template name we want to load - our `home.html` template in the example is simply referred to as `"home"`. This will only work if your templates are in the right folder, so always double check!

To set up a basic controller to serve this template, we created a new class called `HomeController` and annotated it with `@Controller`. As you may remember from the last lesson, this registers the class as a Spring bean *and* makes it eligible for request handling. That's why we can't just use `@Component` - Spring MVC only looks at controllers, not all Spring beans.

In order to actually *bind* the controller to a specific request URL - like `/home` in our example - we have to define a method in the controller and annotate it with `@RequestMapping`. We also have to return a String from this method - this is the name of the template we want to render. For this first step into web development, that's all we do - return the String `"home"` to indicate that we want the `home.html` template to be rendered when a user requests the `/home` URL.



In order to actually render dynamic data in a template, we again need to approach it from both the template and the controller.

In the template, we need to add Thymeleaf *attributes* to our HTML. In our example so far, we added the `th:text` attribute to the heading we want to be dynamic, like so:

```XHTML
<h1 th:text="${welcomeMessage}">Hello, homepage!</h1>
```

This attribute will cause Thymeleaf to replace the text inside the `h1` tag (`Hello, homepage!`) with a string generated by evaluating the expression in the `th:text` attribute (`${welcomeMessage}`). The syntax of this expression is fairly simple: the `${}` indicates an expression to evaluate, and by using a *name* like `welcomeMessage` inside of it, we're telling Thymeleaf to look up a value in the model supplied for this template with the same name.

For that to work, though, we need to add a value named `welcomeMessage` to the model - and we do that in the controller method like so:

```Java
    @RequestMapping("/home")
    public String getHomePage(Model model) {
        model.addAttribute("welcomeMessage", "Hi Hello");
        return "home";
    }
```

First we need to add an argument to the controller method - the `Model` object you see above. This is a special class that Spring MVC will send to Thymeleaf to render the template, and we can set various *attributes* on it to add named values. As you can see, we're adding a value of `"Hi Hello"` to the model with the name `"welcomeMessage"` - which is exactly the name we're referencing in our template! Now when we render the template, the message `Hi Hello` will appear on the web page instead of `Hello, homepage!`

Nice!

We can replace the hardcoded `"Hi Hello"` string in our controller with any Java value or expression, and it will be set every time the controller method is called, which means every time a request comes in for `/home`. That means we can set it dynamically, even based on the request that comes in. If we replace it with `Instant.now().toString()`, we end up with a welcome message that shows the current time, and updates every time we reload the page.



![Spring MVC's architecture. The browser represents the view, and requests from the browser are user actions. When Spring MVC processes a request, it creates a `Model` object that represents the dynamic data associated with the view, and passes it to a controller method that matches the request. The controller updates the model and chooses a template to render in response. Spring MVC passes the template and the updated model to Thymeleaf, which generates an updated view, which Spring sends in response to the browser.](https://video.udacity-data.com/topher/2020/June/5ed975e7_l3-21-mvc-and-you/l3-21-mvc-and-you.png)

**The Spring MVC Architecture**

The figure above shows the Spring MVC's architecture. The browser represents the view, and requests from the browser are user actions. When Spring MVC processes a request, it creates a `Model` object that represents the dynamic data associated with the view and passes it to a controller method that matches the request. The controller updates the model and chooses a template to render in response. Spring MVC passes the template and the updated model to Thymeleaf, which generates an updated view, which Spring sends in response to the browser.

### Key Terms

- **MVC**: MVC is an acronym that stands for **M**odel-**V**iew-**C**ontroller, and it's a common software pattern for user interface design
- **Model**: in MVC, the Model is responsible for maintaining the state of an application,
- **View**: in MVC, the View is responsible for displaying the UI to the user,
- **Controller**: in MVC, the Controller is responsible for processing user actions (sent from the View) to update the Model, and for forwarding those updates back to the View
- **Template**: In software development, templates are used in many different contexts - in general, they are a way to define some often-repeated or reused text or code in a specific format, like HTML, along with *code hooks* that indicate portions of the template that should be replaced dynamically when the template is rendered. In our context, we mostly use Thymeleaf's *HTML templates*, which mostly look like plain HTML with a few extra Thymeleaf-specific attributes. These attributes are our *code hooks*, and allow us to define what data Thymeleaf uses when generating the final HTML from our template.
