+++
title = 'Database'
date = 2024-11-12T07:55:05Z
draft = false
+++

# Database Scaling

- Indexing
    - B-Tree indexes are effective for range queries
    - Fast read and slow write operations
- Matirialized Views
    - pre computed complex query results which are stored to do faster access queries
    - Generally used for business intelligene (BI) or non frequenctly updated data set.
- Denormalization
    - Reduce complex joins to improve query performance
    - Store redundent data to reduce the complexity of database queries and speed up data retrieval.
    - tradeoff: updates must be carefully managed to maintain consistency across the database
- Vertical Scaling
    - Scale database by increase the hardware specs like RAM, CPU cores/freq., storage, etc.
    - Single point of failure
- Caching
    - Store frequently accessed data in a faster storage layer
    - Be Aware of cache invalidation
- Replication
    - create replicas of your primary database on different servers for scaling the reads
    - Synchronous replication
        - data is copied to the replica servers simultaneously as it's written to the primary server ensuring immediate consistency
        - can introduce latency as it waits for write operation in secondary/replica server to complete
    - Asynchronous replication
        - Primary server doesn't wait for replicas to confirm the write on secondary/replica server
- Sharding
    - Splitting a large database into smaller, more manageable pieces, called shards.
    - Each shard is a seperate database that contains a subset of the data.

# ACID

- Atomicity
    - Whatever started can be rolled back
- Consistency
    -  transactions only make changes to tables in predefined, predictable ways.
- Isolation
    -  the concurrent transactions don't interfere with or affect one another.
- Durability
    -  changes to your data made by successfully executed transactions will be saved, even in the event of system failure.

# References

1. [7 Must-know Strategies to Scale Your Database - YouTube](https://www.youtube.com/watch?v=_1IKwnbscQU)