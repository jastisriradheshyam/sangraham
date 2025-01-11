+++
title = 'df (disk free)'
date = 2024-12-15T04:19:52+05:30
draft = false
description = "Information on df (disk free) command"
+++

- `df -k PATH` : prints the filesystem disk space that the specified path resides
  - e.g. `df -k /` -> `/dev/nvme0n1p7  196G  100G   87G  54% /`
  - e.g. `df -k /etc` -> `/dev/nvme0n1p7  196G  100G   87G  54% /`
    - NOTE: result will be different if `/etc` is mounted on separate filesystem

# References & internal citations

1. [inode](../../concepts/file_system/inode.md)
