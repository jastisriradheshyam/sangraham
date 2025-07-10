+++
title = 'Mongo DB Data types'
date = 2025-07-09T17:42:57Z
draft = false
description = 'Information on Mongo DB Data types'
+++

- Boolean
- Null: unknown
- Strings
  - contained within single or double quotes
- Numbers (integers or floating)
  - Int32
  - Int64
  - Double
  - Decimal128
- Objects
- Arrays
  - any data type element.
- Dates
  - represented as a timestamp
  - efficient for querying and sorting
- ObjectId
  - "_id"
  - Unique identifier
  - every document should have this field
  - It's a combination of Timestamp, random value and counter, so that it can have unique value 