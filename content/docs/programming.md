+++
title = 'Programming'
date = 2024-11-12T11:29:11Z
draft = false
+++

# Structural patterns

- Repository Pattern

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


