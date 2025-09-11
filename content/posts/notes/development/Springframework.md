
+++
authors = ["Devendran Nehru"]
title = "Docker Notes"
date = "2025-07-30"
description = "Spring Framework Guide"
tags = [
    "spring",
    "java",
    "dev",
]
categories = [
    "Development",
    "StudyNotes",
]
series = ["StudyNotes"]
+++





## Spring Offerings:


#### IOC
In general, **Tight Coupling** is bad in but most of the time, because it reduces **flexibility and re-usability of code**, it makes changes much more difficult, it impedes test ability
first level: interface
Next level:  spring

IoC enables a framework to take control of the flow of a program and make calls to our custom code.
The advantages of this architecture are:
-   decoupling the execution of a task from its implementation
-   making it easier to switch between different implementations
-   greater modularity of a program
-   greater ease in testing a program by isolating a component or mocking its dependencies, and allowing components to communicate through contracts

IoC patterns:  Strategy design pattern, Service Locator pattern, Factory pattern, and **Dependency Injection (DI)**.

An **IoC container** is a common characteristic of frameworks that implement IoC

 1. **Interface:  ApplicationContext** is where Spring holds instances of objects that it has identified to be managed and distributed
    automatically, instantiating, configuring and assembling as well as
    managing their life cycles. These are called **beans**.
 2. **BeanFactory** - simple rarely used

**Autowiring** - process of wiring dependencies for a spring Bean

**@SpringBootApplication** is a convenience annotation that is equivalent to declaring three separate annotations @Configuration, @EnableAutoConfiguration, and @ComponentScan with their default attributes. It is typically used on the main class of a Spring Boot application to enable auto-configuration, component scanning, and to define the application context.
Before Spring boot, we need to manage using below:
-   **@Configuration**: Indicates that the class is a source of bean definitions for the application context.
    
-   **@EnableAutoConfiguration**: Enables Spring Boot's auto-configuration mechanism, which automatically configures the application based on the dependencies that are added in the classpath.
    
-   **@ComponentScan**: Enables component scanning so that the annotated components are automatically discovered and registered as beans in the application context.


<hr/>

#### Debugging:

Raise debug level for spring framework:    
*application.properties* 

    logging.level.org.springframework=debug

<hr/>

#### Keywords
IOC, DI,  ApplicationContext,

<hr/>

#### References

