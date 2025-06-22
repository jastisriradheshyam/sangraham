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

# References

- [Microservice Architecture Patterns Part 1: Decomposition Patterns | HackerNoon](https://hackernoon.com/microservice-architecture-patterns-part-1-decomposition-patterns)
