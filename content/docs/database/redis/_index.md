+++
title = 'Redis'
date = 2025-06-19T18:26:11.489Z
draft = false
description = "Information on Redis database"
+++

# Redis Cluster

- Data is sharded across multiple Redis nodes
- when working with `redis-cli` use `READONLY` command to get value for a key
- Range queries does not work when in cluster like `SCAN`, `HSCAN`, etc., so get the values one by one.
