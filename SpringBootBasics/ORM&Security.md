![The growing layers of our application. By adding MyBatis, we now have a translation from the Java and Spring world to the world of databases and SQL.](https://video.udacity-data.com/topher/2020/June/5eda82e7_l4-07-big-picture/l4-07-big-picture.png)

**The Growing Layers of Our Application**

The figure above shows the growing layers of our application. By adding MyBatis, we now have a translation from the Java and Spring world to the world of databases and SQL.

### Why a database is required?

Adding a database to our application is a way to externalize data persistence problems. When storing data in memory at runtime, we struggle to deal with:

- Storage Space
- Concurrency
- Persistence of Data

Using a database allows us to isolate these concerns from the rest of our application, so we can focus on the business logic of our application.

### How to interact with a database?

There are many ways to manage the communication between an application and a database. For this course, we'll be using the library [MyBatis](https://mybatis.org/mybatis-3/index.html) *to transform Java objects to SQL query parameters and to transform SQL query results into Java objects.*

We'll create MyBatis Mappers as Spring beans, so we can inject them into any other beans that need them. For example, if we think about an online-shopping example, we might have a UserMapper that manages credentials and profile information and a CartMapper that manages the contents of an individual user's cart. We can inject the UserMapper into a Checkout Service that also receives the CartMapper to apply the charges in a User's cart to that User's stored payment information.

Later in this lesson, we'll combine our MyBatis mappers with Spring Security to authenticate each user's session automatically. To continue our earlier example, this means we could inject the UserMapper in some kind of Authentication Service to check client credentials on login.
