+++
title = 'Misc kubernetes topics'
date = 2025-04-14T15:08:08Z
draft = false
description = "Information on small topics of kubernetes"
+++

# Addon

- `/etc/kubernetes/addons` directory contains the addons in master node

# External DNS

- It creates the DNS record for the cluster in the DNS service provider or service from the cluster.

# Cgroupv2

- Pod spec process
  - Pod -> CRI (containerd/cri-o) -> OCI spec -> OCI runtime (runc) -> systemd (driver) -> cgroupfs kernel
    - Both OCI runtime and diver connects and pass messages from and to cgroupfs

# Security Context

- List
  - `IPC_LOCK`