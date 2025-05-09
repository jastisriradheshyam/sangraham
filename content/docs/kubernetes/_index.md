+++
title = 'Kubernetes'
date = 2024-12-23T06:55:10+05:30
draft = false
description = "Information on Kubernetes"
+++

# Kubernetes commands

- Get pods: `kubectl get pods -A`
- Get services: `kubectl get services -A`
- Force delete the pod: `kubectl delete pods POD_NAME --grace-period=0 --wait=false --force=true`
- Delete service: `kubectl delete services SERVICE_NAME --namespace NAMESPACE`
- Apply YAML file: `kubectl apply -f PATH_TO_CONFIG.yaml`
- Delete using YAML file: `kubectl delete -f PATH_TO_CONFIG.yaml`
- Restart the pods: `kubectl rollout restart deployment -n NAMESPACE DEPLOYMENT_NAME`
- Copy with multiple retries: `kubectl cp --retries=-1 POD_NAME:PATH_INSIDE_POD PATH_ON_HOST`
  - fixes following issue
  ```
  Dropping out copy after 0 retries
  error: unexpected EOF
  ```

## Local development
- Development with local container image:
    - set `imagePullPolicy` as `Never`
    - in `deployment.yaml` : `imagePullPolicy: Never`


## Non frequent commands

- Copy: `kubectl cp LOCAL_PATH NAMESPACE/POD_NAME:PATH_IN_POD`
    - use `-c` argument for specific container

## Exec into certain container

- `kubectl exec -it POD_NAME -C CONTAINER_NAME -- SHELL`


## Drain node

- `kubectl drain NODE_ID`
- will remove all the pod, and other resources from the node, add `--force` to force the removal

## Port Forward

- `kubectl port-forward pods/POD_NAME PORT_IN_LOCAL:PORT_IN_KUBE -n NAMESPACE`
- `kubectl port-forward deployment/DEPLOYMENT_NAME PORT_IN_LOCAL:PORT_IN_KUBE -n NAMESPACE`
- `kubectl port-forward replicaset/REPLICA_SET_NAME PORT_IN_LOCAL:PORT_IN_KUBE -n NAMESPACE`
- `kubectl port-forward service/SERVICE_NAME PORT_IN_LOCAL:PORT_IN_KUBE -n NAMESPACE`

## Kill exec [^3]

- `kill -9 $(pidof kubectl)`
- Add request timeout : `--request-timeout=<value>`

# Related docs

{{< files-list >}}

# References:

1. [linux - How can I use local Docker images with Minikube? - Stack Overflow](https://stackoverflow.com/questions/42564058/how-to-use-local-docker-images-with-minikube)
2. [Copy directories and files to and from Kubernetes Container [POD] | by Nilesh Suryavanshi | Medium](https://medium.com/@nnilesh7756/copy-directories-and-files-to-and-from-kubernetes-container-pod-19612fa74660)
[^3]: [docker - How can I exit a `kubectl exec` command that has frozen due to a network error? - Stack Overflow](https://stackoverflow.com/questions/50939668/how-can-i-exit-a-kubectl-exec-command-that-has-frozen-due-to-a-network-error)
