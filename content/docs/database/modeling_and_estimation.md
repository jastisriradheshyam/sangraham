+++
title = 'Database Modeling and Estimation'
date = 2025-07-09T12:08:26.114Z
draft = false
description = 'Information on Database Modeling and Estimation'
+++

# Understand what will be the workload

1. Identify entities
2. Quantify entities
3. Identify read and writes
4. Quantify read and writes

## 1. Identify entities

Identify entities that will be part of the application.

**For example:** For a book store, there will be books, users, authors, reviews, etc.

## 2. Quantify entities

When modeling data, there should be an estimate how many records will be there for each entity. The estimate can be from existing app utilization, or internal stakeholders planning and estimates or educated guess.

**For example:** Book store entities estimate:

1. Books - 1,000,000
2. Users - 25,000,000
3. Authors - 1,000
4. Reviews - 500,000,000

## 3. Identify read and writes

The entities records are created, updated or deleted during the application lifetime. There should be an identification of what entities are created/Updated (writes) and accessed (reads).

**For example:** Book store entities read and writes:

1. Books
  a. Books are info fetch - read
  b. Create new book record - write
  c. Books edition / price update - write
2. Users - 25,000,000
  a. Add new user - write
  b. fetch user for login and user operation - read
3. Authors - 1,000
  a. create author - write
4. Reviews - 500,000,000
  a. create review - write
  b. update review - write
  c. fetch review - read

## 4. Quantify read and writes

Quantify read and writes on the entities. At what rate the entities are accessed or written to. Similar to entities quantification, the estimates can be from existing app utilization, or internal stakeholders planning and estimates or educated guess. 

1. Books
  a. Books are info fetch - read - 1000/s
  b. Create new book record - write - 2/day
  c. Books edition / price update - write - 10/month
2. Users - 25,000,000
  a. Add new user - write - 1/s
  b. fetch user for login and user operation - read - 1/min
3. Authors - 1,000
  a. create author - write - 1/month
4. Reviews - 500,000,000
  a. create review - write - 50/s
  b. update review - write - 1/s
  c. fetch review - read - 200/s

# Relationships

1. one-to-one
2. one-to-many
3. many-to-many