+++
title = 'Service Discovery'
date = 2025-04-14T15:31:44Z
draft = false
description = "Service discovery in kubernetes"
+++

- The DNS service can be used to find other services running on the same cluster
- A container in the same pod can connect the port of the other container directly using **`localhost:port`**
- **Service** definition is required for DNS to work

- `service-name.NAMESPACE`
  - `service-name.NAMESPACE.svc.cluster.local`

- DNS is managed by `kube-dns` service hosted in `kube-system` namespace