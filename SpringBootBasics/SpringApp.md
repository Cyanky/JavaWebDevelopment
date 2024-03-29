Spring is an *application framework*, which means that instead of choosing when to invoke it from your application, you choose when it invokes your application code. This pattern of software development is called Inversion of Control (IoC), and it's powerful because it allows developers to develop specialized application components and use Spring to connect them with each other using dependency injection. This is good for clean, separated code and for code reuse. This is evident when looking at the vast number of Spring modules and Spring-integrated third-party tools that are available. This course focuses on a few of them:

- **Spring MVC**, a generic web controller library for Spring that supports a wide variety of utilities to simplify the handling of HTTP requests
- **Thymeleaf**, a third party template engine that can integrate with Spring MVC to simplify the generation of web pages as responses to HTTP requests
- **Spring Security**, a generic authentication library for Spring that can integrate with many different credential sources and authentication protocols to automatically manage request authentication and security contexts
- **MyBatis**, a third-party database access library that provides simple SQL/Java mapping tools that can be defined in Spring components

### The End of Boilerplate: Spring Boot

So Spring adds a lot of features, but it still sounds like a lot of configuration. We still have to deploy it to an application server, right? And we still have to create a servlet for Spring to live in. It also sounds like getting all of these modules and utilities to work together might take some work.

In the past, Spring did require a lot of configuration, but over time, the development world has moved towards a convention-over-configuration approach. Spring Boot is a project that provides an a-la-cart Spring experience, complete with a web page for generating and downloading starter projects based on the application needs. Most Spring Boot applications today also contain an embedded application server with a default, pre-configured servlet definition. All you have to do to run your Spring-enabled code as a server is to run a main method.

With the rise of containerized architectures like Docker, this style of application development has become as popular as the pluggable application server, and in this course, we'll be exclusively using this mode. However, if you do want to deploy your Spring Boot application to a traditional application server, there are built-in tools that allow you to package the application as a standard WAR file.

### Key Terms

- **IoC**: Inversion of Control, which is the practice of designing libraries as *application runners*. This allows developers to focus on application-specific logic and rely on IoC containers to connect application components with one another, eliminating a lot of boilerplate and encouraging a clean separation of development concerns.
