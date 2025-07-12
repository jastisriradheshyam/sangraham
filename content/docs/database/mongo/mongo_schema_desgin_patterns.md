+++
title = 'Mongo DB Schema Design patterns'
date = 2025-07-09T17:42:57Z
draft = false
description = 'Information on Mongo DB Schema Design patterns'
+++

# Inheritance pattern

- Helps to groups similar document in same collection.
- Inheritance patterns is based on the notion: Polymorphism. Documents can have different forms or shape.
- There will be a field which helps in identifying the form/shape of the document in the collection. 

## When to use

- When there are more similarities then differences in the entities.
- When documents needs to be kept together in the same collection to read them together.

## How to apply

Use the aggregation framework to apply the inheritance pattern

## Example

Book store app, where books can be audio book, printed book, and ebook.

```json
{
    ...
    "title": "", // common
    "author": "", // common
    "authorId": "", // common
    "rating": 4, 
    "genres": [""], // common
    "pages": 0,
    "price": 0, // common
    "publisher": "", // common
    ...
    "product_type":"ebook", // Defines the type of document
    "download_url": "",
}
```

Audiobook where there are audiobook specific fields.
```json
{
    ...
    "download_url":""
    ...
    "product_type": "audiobook",
    "narrators": [""],
    "duration": "",
    "time_by_chapter": [{"chapter": "","end":""}]
}
```

```json
{
    ...
    "product_type": "printedbook",
    // no requirement of download_url so remove it.
}
```

Consider if there is no product type is not present in the books collection but all three types of books are present in the collection then aggregation pipeline can be applied to add product type field.


```js
var apply_inheritance_pattern_to_books_pipeline = [
    $project: {
        _id: "$_id",
        product_id:: "$product_id",
        product_type: {
            $ifNull: ["$product_type", "unspecified"],
        }, // just adding product type field with unspecified value.
        description: {
            $ifNull: [
                "$desc",
                "$description",
                "$details",
                "Unspecified",
            ]
        },
        authors: {
            $ifNull: [
                "$authors",
                ["$authors"],
                "Unspecified",
            ],
        },
        publisher: "$publisher",
        ...
    },
    {
        $merge: {
            into: "books",
            on: "_id",
            whenMatched: "replace",
            whenNotMatched: "discard",
        },
    },
]

db.books.aggregate(apply_inheritance_pattern_to_books_pipeline)
```

```js
var cleanup_audiobook_entries_in_book_pipeline = [
    {
        $match: {
            $and: [{product_type: "Unspecified"},{length_minutes: {$gte: 0}}],
        },
    },
    {
        $set: {product_type: "audiobook"},
    },
    {
        $merge: {
            into: "books",
            on: "_id",
            whenMatched: "replace",
            whenNotMatched: "discard",
        },
    },
];
```


# Computed Pattern

- Run expensive operations when the data changes and store the results for quick access.

Common computations:

- Mathematical
- Roll-up

Mathematical:

- Pre-compute on write

For example rating

```
NewAverage = (avgRating*reviewCount + newRating)/(reviewCount+1) 
```

Roll-up:

Merging data together. Allows view data as a whole.

```js
use bookstore;

var rollup_product_type_and_number_of_authors_pipeline = [
    {
        $group: {
            _id: "$product_type",
            count: {
                $sum: 1,
            },
            averageNumberOfAuthors: {
                $avg: {
                    $size: "$authors",
                },
            },
        },
    },
]

db.books.aggregate(rollup_product_type_and_number_of_authors_pipeline )
```

# Extended Reference pattern

Embed data from other documents into main document to reduce `lookup` (equivalent of joins in SQL) operation on each query.

# Approximation Pattern

This pattern generates statistically valid number that is not exact

- Reduces writes
- and in some cases reduce contention on heavily updated documents

## When to use

- When data is either difficult or expensive to calculate, 
- and getting the exact number is not critical for the use case.
- well suited for big data

# Anti-patterns

- Unbounded Arrays
    - When the array is expected to grow without bound
- Bloated Documents
    - WiredTiger: default mongo db storage engine, keeps data that is accessed frequently in memory. 