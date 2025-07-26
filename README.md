# 🧠 Inversion of Control (IoC) & Dependency Injection (DI) in Spring

## 🔄 Inversion of Control (IoC)

**IoC** is a design principle where framework takes the control of flow of the program rather than by the developer, Spring IOC Container is responsible for creating, configuring, and managing the lifecycle of objects called beans.

### 🌱 Key Points:
- The framework manages object lifecycle (creation, configuration, destruction).
- Objects managed by the container are called **Beans**.
- Promotes loose coupling and easier scalability.

### 📦 Containers in Spring:

| Type              | Description                                                                 |
|-------------------|------------------------------------------------------------------------------|
| `BeanFactory`      | Basic container that instantiates and configures beans                     |
| `ApplicationContext` | Advanced container with features like internationalization, event handling, and integration with Spring tools |

---

## ⚙️ Dependency Injection (DI)

**DI**-Dependency inJection is a design pattern and a part of IOC, DI is the way we implement IOC.
It allows Spring to inject required dependencies into objects rather than the object instantiating them itself.

### 🎯 Purpose:
- Promotes separation of concerns
- Improves testability
- Reduces boilerplate

---

## 🛠️ DI Types & Examples
1. _Constructor injection_
   -> Gives dependencies to the object when it is created, ensuring they are ready to use immediately
   -> It makes sure all the needed dependencies are available right away
2. _Setter Injection_
   -> Gives dependencies to setter method after object is created allowing changes later
   -> It allows for more flexibility for changing or adding dependencies later

### 1️⃣ Constructor Injection

Injects dependencies when the object is created—ensures they're available right away.

#### 📋 Example:
```java
@Component
public class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```
2️⃣ Setter Injection
Injects dependencies using a setter method—allows flexibility to change or add later.

```java
@Component
public class Car {
    private Engine engine;

    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}
```
👇 Autowiring in Another Component
```java
@Component
public class Vehicle {
    private final Engine engine;

    @Autowired
    public Vehicle(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Vehicle is driving");
    }
}
```
👇 Spring Boot Main Application
```java
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(DemoApplication.class, args);
        Vehicle vehicle = context.getBean(Vehicle.class);
        vehicle.drive();
    }
}
```
# 🧠scope of beans

In Spring Framework, “scope” defines the lifecycle and visibility of a bean within the Spring container. The scope determines when and how a bean is created, and how it is shared among different parts of an application. Choosing the right bean scope is crucial for efficient resource management and optimal performance. In this article, we will delve into the various predefined bean scopes provided by Spring and illustrate their usage with examples.

## Predefined Bean Scopes

Spring provides several predefined bean scopes that dictate the lifecycle of beans. These are:

**1. Singleton (Default)
2. Prototype
3. Request
4. Session
5. Application
6. WebSocket
**

### Singleton Scope
The Singleton scope is the default scope in Spring. In this scope, the Spring container creates a single instance of the bean, and this instance is shared across the entire application.

Characteristics:
- Single instance per Spring IoC container.
- Shared and reused across the application.

Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
@Configuration
public class AppConfig {
@Bean
 public MyService myService() {
 return new MyService();
 }
}
```
In this example, the `myService` bean is defined with the default singleton scope. Every time `myService` is requested, the same instance is returned.

### Prototype Scope
The Prototype scope creates a new instance of the bean each time it is requested from the container.

Characteristics:
- New instance each time the bean is requested.
- Not shared; each request gets a unique instance.

Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@Configuration
public class AppConfig {
 @Bean
 @Scope("prototype")
 public MyService myService() {
 return new MyService();
 }
}
```
In this example, the `myService` bean is defined with the prototype scope. A new instance is created every time `myService` is requested.

### Request Scope
The Request scope is specific to web applications. In this scope, a new bean instance is created for each HTTP request and is shared within that request.

Characteristics:
- Single instance per HTTP request.
- Used in web applications.

Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;
import org.springframework.web.context.WebApplicationContext;
@Configuration
public class AppConfig {
@Bean
 @Scope(WebApplicationContext.SCOPE_REQUEST)
 public MyService myService() {
 return new MyService();
 }
}
```
In this example, the `myService` bean is defined with the request scope. A new instance is created for each HTTP request.

### Session Scope
The Session scope is also specific to web applications. In this scope, a new bean instance is created for each HTTP session and is shared within that session.

Characteristics:
- Single instance per HTTP session.
- Used in web applications.

Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;
import org.springframework.web.context.WebApplicationContext;
@Configuration
public class AppConfig {
@Bean
 @Scope(WebApplicationContext.SCOPE_SESSION)
 public MyService myService() {
 return new MyService();
 }
}
```
In this example, the `myService` bean is defined with the session scope. A new instance is created for each HTTP session.

### Application Scope
The Application scope is specific to web applications running in a Servlet context. In this scope, a single bean instance is created for the lifecycle of the Servlet context and is shared across the entire context.

Characteristics:
- Single instance per Servlet context.
- Used in web applications.

Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;
import org.springframework.web.context.WebApplicationContext;

@Configuration
public class AppConfig {
@Bean
 @Scope(WebApplicationContext.SCOPE_APPLICATION)
 public MyService myService() {
 return new MyService();
 }
}
```
In this example, the `myService` bean is defined with the application scope. A single instance is created for the entire Servlet context.

### WebSocket Scope
The WebSocket scope is specific to WebSocket communication. In this scope, a new bean instance is created for each WebSocket session.

Characteristics:
- Single instance per WebSocket session.
- Used in applications with WebSocket communication.

Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;
import org.springframework.web.socket.config.annotation.EnableWebSocket;
@Configuration
@EnableWebSocket
public class AppConfig {
@Bean
 @Scope("websocket")
 public MyService myService() {
 return new MyService();
 }
}
```
In this example, the `myService` bean is defined with the WebSocket scope. A new instance is created for each WebSocket session.

Custom Scopes
Spring also allows for the creation of custom scopes if the predefined scopes do not meet the application’s requirements. Custom scopes can be defined by implementing the `Scope` interface.


Conclusion
Understanding the different bean scopes provided by Spring is essential for designing efficient and scalable applications. By choosing the appropriate scope for your beans, you can optimize resource management, performance, and application behavior. The predefined scopes cover a wide range of use cases, from singleton and prototype to request, session, application, and WebSocket scopes, each serving specific needs in both standard and web applications.

Selecting the correct bean scope will depend on the specific requirements of your application, such as the need for shared instances, resource management, and the expected lifecycle of the beans within your application context. By leveraging the right scope, you can ensure that your Spring application is both efficient and maintainable.
