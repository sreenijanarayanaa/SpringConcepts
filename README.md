**=>   IOC(Inversion of control)**
It is a concept/design principle where the framework takes the control of flow of execution.
The control of object creation and lifecycle is managed by the framework or the container rather than by the developer.
It is responsible for creating, configuring and managing the lifecycle of objects called beans.
There are two types
1. _Bean factory:_
It is a basic container that handles creating and managing of beans

2. _Application context:_
Application context is more advanced one which includes features like event handling and can be easily integrated with spring tools

**=>   DI(Dependency Injection)**
Dependency inJection is a design pattern and a part of IOC, DI is the way we implement IOC.
It allows objects to be injected with their dependencies rather than us creating those dependencies.
There are 2 types of DI's:
1. Constructor injection
2. Setter Injection
   
_1. Constructor injection_
   -> Gives dependencies to the object when it is created, ensuring they are ready to use immediately
   -> It makes sure all the needed dependencies are available right away
_2. Setter Injection_
   -> Gives dependencies to setter method after object is created allowing changes later
   -> It allows for more flexibility for changing or adding dependencies later

