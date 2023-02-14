## Spring Boot IoC Configuration


Under the hood, Spring is just a Java application itself - and it responds to our configuration in a predictable way. When a Spring application starts, it scans your code base for specially-marked class files and configuration options. It uses that information to instantiate your application components as Java objects, and it stores them in a special data structure called the application context. This context is ultimately very similar to a `Map` or a python dictionary, and it can be queried at runtime to find specific components when needed. This is a closed system, so components instantiated outside of Spring won't automatically be injected with dependencies like those instantiated by Spring. Mind the `new` keyword!


## Annotations to begin the Setup process

In a Spring Boot application, the basic setup of the Spring application context has already been done for us. The following annotations are the starting point of an application:

1. **`@SpringBootApplication`** - In a generated project starter, you're always given a main application class with the `@SpringBootApplication` annotation. This annotation is actually equivalent to three other annotations from Spring: `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`. The `@SpringBootApplication` configures Spring's component scanning and auto-configuration.

1. **`@Configuration`** - It tells Spring that the annotated class includes component definitions for Spring to process. These take the form of `@Bean`-annotated method whose return values are included as components in the application context. These methods can also take parameters, which act like the dependencies of the components returned by the methods.

1. **`@EnableAutoConfiguration`** - It tells Spring that it's okay to try to match dependencies to components automatically. Usually, that means dependencies are filled based on type, so in the example above, we have the `compoundMessage` method which depends on the `basicMessage` implicitly - the only String bean that Spring is aware of when constructing the `compoundMessage` is the `basicMessage`, so it uses that.

When there are multiple beans that satisfy a specific dependency, Spring's auto-configuration needs some help to decide which to use. A common solution is to mark a bean with the `@Primary` annotation to indicate a universally-preferred bean for its type. Or, you can use pairs of `@Qualifier` annotations on beans and the dependencies that reference them to gain a finer level of control.

`@ComponentScan` provides another layer of automation - automatic component scanning throughout your entire code base. 

![An example of how Spring processes an IoC configuration. A bean without dependencies is initialized first and placed within the application context. A service is instantiated by Spring, and the first bean is retrieved from the app context to be injected as a dependency, after which Spring places the service in the application context. Finally, another bean is initialized by Spring, which retrieves the previous two components to be injected as dependencies, after which the new bean is placed in the app context, and the application is fully initialized.](https://video.udacity-data.com/topher/2020/June/5ed946f4_screen-shot-2020-06-04-at-12.08.59-pm/screen-shot-2020-06-04-at-12.08.59-pm.png)

**How Spring Processes an IoC Configuration.**

The figure above shows an example of how Spring processes an IoC configuration. The general steps are:

- A bean without dependencies is initialized first and placed within the application context.
- A service is instantiated by Spring, and the first bean is retrieved from the app context to be injected as a dependency, after which Spring places the service in the application context.
- Finally, another bean is initialized by Spring, which retrieves the previous two components to be injected as dependencies, after which the new bean is placed in the app context, and the application is fully initialized.

### Key Terms

- **Configuration Files**: Project files that configure some part of Spring's operation. Some are embedded in Java classes, like we just discussed, and others are `.properties`, `.yaml`, and `.xml` files that we'll discuss later this lesson. Some of them configure the IoC context, like the ones we just discussed, and others configure more abstract pieces of Spring's system.
- **Component Annotations**: Component annotations are annotations that identify application components for Spring to manage. `@Bean` and `@Configuration` are examples from the most recent videos, and in the next section we'll discuss `@Component` and `@Service` as well.
- **Application Context**: Spring's application context is just a giant data structure that holds all application component instances. It can be queried to gain access to a specified component at runtime, and it's what Spring uses to resolve dependencies.
- **Beans**: "Beans" are Spring's name for generic application components, and include any value Spring has stored in the application context. A bean is always either an object or primitive value.
- **Closed System**: Spring's application context is a closed system, which means that it manages all of the components stored within. It is not possible to instantiate a component manually and still link it fully with Spring - it will never be aware of the components inside of Spring's application context, and vice versa.
- **`@SpringBootApplication`**: An annotation put on the main application class of a Spring Boot project. It serves as an alias of three other annotations, `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`
- **`@Configuration`**: A class annotated with `@Configuration` is instantiated and managed by Spring as a component, but also as a bean factory. Any methods of the configuration class that are annotated with `@Bean` are used by Spring to create new beans to add to the application context.
- **`@Bean`**: A method annotated with `@Bean` inside of a configuration class will be used by Spring to generate a bean of the method's return type. This means that the developer can manually configure beans to be included in the application context.
- **`@EnableAutoConfiguration`**: A class annotated with `@EnableAutoConfiguration` tells Spring to try to automatically match beans to dependencies based primarily on type. This reduces the need for boilerplate code explicitly identifying individual beans as dependencies.
- **`@Primary`**: This annotation distinguishes the annotated bean method as the default dependency of its type. This is used to resolve conflicts that arise from having multiple bean definitions of the same type when auto configuration is enabled.
- **`@Qualifier`**: This annotation distinguishes the annotated bean method or dependency declaration as a qualified bean or dependency. Qualified beans are considered for unqualified dependencies, but only matching qualified beans are considered for qualified dependencies. 
