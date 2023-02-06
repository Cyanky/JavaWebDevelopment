Spring Boot is best experienced with the help of Spring Initializr, an official project generator. You can use it to configure metadata and build properties of a project as well as what starter dependencies you want to include. These include:

- [Spring Dev Tools](https://docs.spring.io/spring-boot/docs/1.5.16.RELEASE/reference/html/using-boot-devtools.html): utilities including hot reloading changed code into a running application
- [Spring MVC](https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/mvc.html): web layer utilities that make developing server-side web apps easy
- [Spring Data](https://spring.io/projects/spring-data): a common interface for many different types of database access
- And [many more](https://spring.io/projects) Once you've selected your dependencies and chosen your language, build tool, and project identifiers, Spring Initializr will generate a zip file that includes a ready-to-run server with all of the choices you made reflected in its `pom.xml` file, as well as the package structure.

## Key Terms

- **Maven**: A dependency management system and project build tool for Java. Provides a standardized way to define dependencies between projects and include them in the project build path.
- **POM**: The **P**roject **O**bject **M**odel that Maven uses to represent the dependency and build configuration of a project. Usually, this refers to the `pom.xml` configuration file found in a Maven project.
- **Dependency Management System**: Any tool that automates the downloading and linking of external packages to a software development project. Most languages these days either provide one officially or have a community-accepted standard.
