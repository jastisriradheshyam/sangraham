+++
title = 'Labels'
date = 2025-04-14T15:19:41Z
draft = false
description = "Labels in Kubernetes"
+++

# Node Labels

- view the node labels
  - `kubectl get node --show-labels`
- set the node labels
  - `kubectl label nodes node1 hardware=high-spec`
  - `kubectl label nodes node2 hardware=low-spec`

- Select the node for pod deployment

```yaml
spec:
...
  nodeSelector:
    hardware: high-spec
```