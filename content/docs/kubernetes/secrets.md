+++
title = 'Secrets'
date = 2025-04-14T15:30:25Z
draft = false
description = "secrets in kubernetes"
+++

- Internal API's also uses Secrets mechanism

# Examples

```yaml
- name: SOME_ENV_VAR
  valueFrom:
    secretKeyRef:
      name: secrets-object-name
      key: key-name-in-the-secrets-object
```

```yaml
volumeMounts:
  - name: credVolume
    # will create files with value with key as filename
    mountPath: /some-path
    readOnly: true
volumes:
  - name: credVolume
  secret:
    secretName: secrets-object-name
```

# Types

- `Opaque`