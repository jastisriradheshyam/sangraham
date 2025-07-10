+++
title = 'Mongo DB'
date = 2025-07-09T17:42:57Z
draft = false
description = 'Information on Mongo DB principles'
+++

Data that is accessed together should be stored together

Data entities are stored in **documents**

Collections: Organize related documents

document model is inherently flexible. The document acts as the schema. This allows to create similar but different schemas for the same set of entities depending on the needs of the application.

Mongo DB stores data in BSON format, its a binary format of json.
- It is an extension to JSON
- If provide additional datatype like: Date, ObjectId and Timestamps

# Core design principles

1. Polymorphism
  a. Ability to store documents with different fields in the same collection.
2. Easy to work with arrays
  a. The value of a field in a document can be an array of values which can themselves be documents.
3. Embedding
  a. Embedding related documents into a parent document to represent relationships.

# Architecture

```
Cluster
  ↑
Node
  ↑
Database
  ↑
Collection
  ↑
Document
```

- **Document**
  - Smallest unit of data in mongodb
  - Stores data in object and any related metadata
  - Data is stored in field-value (key-value) pairs

- **Collection**
  - A collection is a group of documents that correspond to an entity
  - Can support multiple entities and different shapes

- **Database**
  - A group of collections

- **Node**
  - A individual mongo db instance

- **Cluster**
  - Two type of clusters
    - Replica sets
      - High availability through replication
    - Shared cluster
      - Scaling through partitioning process called sharding
  
## Consistency in distributed setup

Mongo DB manages data consistency through read and write concerns

- Read Concern
  - Read Concern controls the consistency and isolation of the data read from replica sets or sharded clusters
  - By default read concern is set to "local", this means mongo db will return the data from the node on which the request was run, without waiting for acknowledgment from replica set members.
    - This ensures high availability and low latency, but cannot guaranty consistency.
  - The majority setting in read concern increases consistency.

- Write concern
  - Write concern dictates the number of replica set members that must confirm a write operation.
  - By default write concern setting is set to majority.
    - Majority of the replica set confirms the write is successful

## Sharding

- Sharding provides horizontal scalability
- Add more shards to distribute the data

# Limits

- Maximum document size of 16MB
-  In single document there can be maximum of 100 levels of nesting

# Schema Validation

- Define rules and constraints
- Executed on the database layer
- Works with polymorphic collections and embedded documents

# Guidelines for embedding and referencing

Here MongoDB golden rule of schema design is preferred: Data that is accessed together should be stored together

| Guidelines            | Description | Yes ✅ | No ❌ |
| --------------------- | ----------- | ------- | ----- |
| 1. Simplicity         | Would keeping the pieces of information together lead to a simpler data model and code? | Embed | Reference |
| 2. Go together        | Do the pieces of information have a "has-a", "contains", or similar relationship? | Embed | Reference |
| 3. Query Atomicity    | Does the application query the pieces of information together | Embed | Reference |
| 4. Update complexity  | Are the pieces of information updated together | Embed | Reference |
| 5. Archival           | Should the pieces of information be archived at the same time | Embed | Reference |
| 6. Cardinality        | Is there a high cardinality (current or growing) in the child side of the relationship | Reference | Embed |
| 7. Data duplication   | Would data duplication be too complicated to manage and undesired | Reference | Embed |
| 8. Document size      | Would the combined size of the pieces of information take too much memory or transfer bandwidth for the application? | Reference | Embed |
| 9. Document growth    | Would the embedded piece grow without bound? | Reference | Embed |
| 10. Workload          | Are the pieces of information written at different times in a write-heavy workload | Reference | Embed |
| 11. Individuality     | For the child side of the relationship, can the pieces exist by themselves without a parent? | Reference | Embed |