+++
title = 'Microservices'
date = 2024-12-14T14:58:48+05:30
draft = false
description = 'Information on Microservices Architecture'
+++

# Decomposition patterns

- Microservices decomposition by business capability
- Microservices decomposition by subdomain
- Microservices decomposition by transaction

## Microservices decomposition by business capability

- Services decomposed based on business units
  - For example Banking application has Account management, transaction processing, loan origination, card management, etc.

## Microservices decomposition by subdomain

- Microservices are defined by subdomain decomposition pattern, where each microservice is processing for each subdomain.
  - for example Purchasing and claims microservices under sales domain

## Microservices decomposition by transaction

- Microservices defined by transactions, like order management, payment management, etc. within a E-Commerce platform.
- This reduces two-phase commit problems.

# General Questions

## 1. Consider the effect of modularization on the delivery of software. Will it take more or less time to get a tightly coupled monolithic block of software to the required quality compared with a system designed as very loosely coupled modules or microservices? What are the advantages or disadvantages of each approach? - Question from Pragmatic Engineer (20 year edition)

🧱 Monolithic architecture

Delivery Time
- Faster initially: easier to build and deploy in the early stages because everything is in one place
- Slower over time: As complexity grows, changes become riskier and harder to test.

Advantages
- Simpler to develop and deploy initially.
- Easier debugging due to single codebase.
- Performance can be better due to fewer network calls.

Disadvantages
- Tight coupling makes changes risky.
- Harder to scale individual components.
- Difficult to adopt new technologies incrementally.
- Longer regression cycles as everything is tested together.

🧩 Modular / Microservice architecture

Delivery Time
- Slower initially: Requires more planning, infrastructure, and coordination.
- Faster over time: Teams can work independently, deploy frequently, and scale efficiently.

Advantages
- Loose coupling improves maintainability and flexibility.
- Easier to scale and optimize individual services.
- Fault isolation: one service failing doesn't bring down the whole system.
- Enables continuous delivery and deployment.

Disadvantages
- More complex infrastructure (e.g., service discovery, monitoring, logging).
- Requires strong DevOps practices.
- Network latency and inter-service communication issues.
- Harder debugging across services.

🕰️ Quality and time trade-off

| Aspect                 | Monolith     | Microservice    |
| ---------------------- | ------------ | ----------------|
| Initial Delivery Speed | ✅ Faster   | ❌ Slower       |
| Long term Agility      | ❌ Slower   | ✅ Faster       |
| Testing Complexity     | ❌ High (all in one) | ✅ Isolated per service |
| Deployment             | ❌ All-or-nothing | ✅ Independent per service |
| Scalability            | ❌ Limited        | ✅ Granular   |
| Team Autonomy          | ❌ Low            | ✅ High       |

🧠 Strategic considerations
- Small teams or MVPs -> Monolith might be more practical.
- Large teams or evolving products -> Microservices offer better scalability and maintainability.
- Hybrid approach -> Start with a modular monolith and evolve into microservices as needed.

# References

- [Microservice Architecture Patterns Part 1: Decomposition Patterns | HackerNoon](https://hackernoon.com/microservice-architecture-patterns-part-1-decomposition-patterns)
