+++
title = 'Certbot'
date = 2024-12-15T04:14:08+05:30
draft = false
description = "Information on Certbot"
+++

- For New Non-Interactive Certificate : `certbot certonly -n --webroot --domains DOMAIN_NAME -m MAIL_ID`
  - domains argument accept multiple domain with comma seperated values
- For interactive session with standalone server: `sudo certbot certonly --standalone`
