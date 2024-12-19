+++
title = 'SOLID'
date = 2024-12-14T15:01:02+05:30
draft = false
+++

**SOLID (Single Responsibility, Open Close Principle, Liskov Substitution, Interface Segregation, Dependency Inversion)**

# Single Responsibility

A class should only have one reason to change. This minimizes the impact of modifications.

## Advantages

- Easier to understand and maintain
- Writing unit test cases for the class becomes easier
- it provides flexibility as change in one responsibility / class don't affect unrelated parts of the system

# Open–closed principle

An class / any software entity should be open for extension, but closed for modification.

## Advantages

- It maintains code stability and reduce bugs

# Liskov substitution principle

Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.
function / functions that use pointers or references to base class must be able to use objects of derived classes without knowing it. in terms of class, objects of a superclass should be replaceable with objects of subclasses without affecting the program's correctness.
A subclass can replace a superclass, if and only if, the subclass does not change the functionality of the superclass.

# Interface segregation principle

Clients should not be forced to depend upon interfaces they do not use.

## Advantages

- Encourages creating multiple, specific interfaces rather than a single, general purpose interface
- It prevents a class from being forced to implement interface it doesn't use. Reducing the side effects of changes in unrelated interfaces.

# Dependency inversion principle

High level modules shouldn't depend on low level modules. Both should depend on abstractions.
Abstractions should not depend on details. Details should depend upon abstractions.
Class should depend on interfaces rather then concerte classes.

# Clean architecture

- Seperation of concerns
    - Each level in your program should be seperated by a clear barrier, the transport layer, the service layer, the storage layer, etc.

- Dependency Inversion Principle (DIP)
    - You're injecting the dependencies in your layers. You dont directly call them.
    - Why? It promotes loose coupling and makes it easier to test our programs.

- Adaptability to change
    - By organizing the code in a modular and flexible way, we can more easily introduce new features, refactor existing code, and respond to evolving business requirements.
    - Systems should be easy to change, if we have to change a lot of existing code to add a new feature then we are doing it wrong.

- Focus on business value
    - Focus on delivering value to your users, they are the ones who will be paying bills at the end of the month.

# Additional Links

1. [Clean Coder - Getting a SOLID start.](https://sites.google.com/site/unclebobconsultingllc/getting-a-solid-start)
2. [Design Principles and Design Patterns](https://web.archive.org/web/20150906155800/http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf)
