+++
title = 'CAP Theorem'
date = 2024-12-14T14:58:48+05:30
draft = false
description = 'Information on CAP Theorem'
+++

CAP (Consistency, Availability, Partition Tolerance)

In a distributed data store, we can only guarantee two out of three of these properties
- Consistency
- Availability
- Partition Tolerance

# Consistency

Every read gets the most recent write or returns an error.

# Availability

Every request gets a response and be available, even if it's not the latest data.

# Partition Tolerance

System stays operational even when there are network faults.
