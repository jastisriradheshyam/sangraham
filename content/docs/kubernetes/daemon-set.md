+++
title = 'Daemon Set'
date = 2025-04-14T15:14:35Z
draft = false
description = "Daemon set in kubernetes"
+++

- A DaemonSet ensures that all or some nodes run a copy of a pod.
- Got Stabe in K8 version 1.7

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  ...
spec:
  ...
  # Configuration similar to pod
```