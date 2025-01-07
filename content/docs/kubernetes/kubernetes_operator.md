+++
title = 'Kubernetes Operator'
date = 2024-12-23T06:55:21+05:30
draft = false
+++

Operator is a design pattern for extending the API of a Kubernetes cluster to include a new resource type that you define the behavior of. This resource can then be used in the same manner as Kubernetes core resources.

Benifits

1. New resource is available for use on the cluster in the exact same manner as core resources such as pods and services.
2. Expressive power that comes with having control over the internal reconciliation of your new resource.Rather than having your application statically deployed on a cluster, operators enable you to react both to requested changes
from users and a cluster’s shifting circumstances to manage your custom resource.

# Tools for writing an operator

1. [Operator SDK](https://github.com/operator-framework/operator-sdk)
    - CLI tool for scaffolding operators that is based on Kubernetes
2. [Kubebuiler](https://github.com/kubernetes-sigs/kubebuilder)
    - A tool for scaffolding Golang operators
3. [Controller Runtime](https://github.com/kubernetes-sigs/controller-runtime)
    - A Golang library that is a simplified wrapper around Client-go, the Kubernetes API Golang client library

# Architecture

At its heart, a Kubernetes cluster is really just a few components wrapped around an etcd key-value store.

1. When you issue the command `kubectl create foo`, your local command-line interface issues a write request to the Kubernetes API server.
2. The API server performs validation to ensure that your `foo` object has the structure it should, but mostly just passes your request on through to the **etcd** store.
3. Your request creates a new entry in **etcd** for that resource.
4. This change is seen by a Kubernetes controller, which is a process responsible for reconciling the desired state contained in the **etcd** store with the actual state running in the cluster.
5. When the controller sees your new entry, it goes and performs whatever actions are needed to create the desired state of your object `foo`. Once it has reconciled the desired state from the **etcd** with the actual state of the system, it marks the entry in the **etcd** as `reconciled`.
