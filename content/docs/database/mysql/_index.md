+++
title = 'MySQL'
date = 2025-04-14T15:39:08Z
draft = false
description = "Information on MySQL"
+++

# Add user:

```sql
CREATE USER 'radhe'@'%' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
```
# update the host access:

```sql
UPDATE mysql.user SET Host='%' WHERE Host='localhost' AND User='root';
UPDATE mysql.db SET Host='%' WHERE Host='localhost' AND User='root';
FLUSH PRIVILEGES;
```

# ONLY_FULL_GROUP_BY

- `vi /etc/mysql/my.cnf`
- add this to the file
```conf
[mysqld]
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
```
- Restart the MySQL deamon/server
  - `sudo systemctl restart mysql`

# References:
- https://drib.tech/programming/turn-off-sql-mode-only_full_group_by-mysql-5-7
