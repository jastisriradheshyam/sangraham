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

# Core design principles

1. Polymorphism
  a. Ability to store documents with different fields in the same collection.
2. Easy to work with arrays
  a. The value of a field in a document can be an array of values which can themselves be documents.
3. Embedding
  a. Embedding related documents into a parent document to represent relationships.


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