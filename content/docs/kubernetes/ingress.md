+++
title = 'Ingress'
date = 2025-04-14T15:18:43Z
draft = false
description = "Ingress in kubernetes"
+++

- kind: `Ingress`
- Part of k8 since v1.1
- Alternative to `Loadbalancer` and `nodePorts`
- Ingress controller is a pod
- On of the ingress controller is NGINX and it is hosted by using `ReplicationController` kind config file
- Only works for HTTP and HTTPS connections
- Shows the pods with `app.kubernetes.io/name=ingress-nginx` labels
    - `kubectl get pods --all-namespaces -l app.kubernetes.io/name=ingress-nginx`

# Nginx Based annotations

- `kubernetes.io/ingress.class: "nginx"`
- `nginx.ingress.kubernetes.io/use-regex: "true"`
- 
  ```conf
  nginx.ingress.kubernetes.io/server-snippet: |
    proxy_intercept_errors on;
    error_page 404 = @custom_404;
      
    location @custom_404 {
      proxy_set_header X-Code $status;
      return 404 'Hey, resource not found!';
    }
  ```

# References

- https://www.callumpember.com/Easy-Kubernetes-Nginx-Ingress-Custom-Error-Pages/