+++
title = 'Grubby'
date = 2024-12-19T19:28:25+05:30
draft = false
description = "Information on Grubby command"
+++

- It is a tool to handle Grub boot manager

- List Grub kernel parameters `sudo grubby --info=ALL`
- Update specific key value pair in kernel parameters: `sudo grubby --update-kernel=ALL --args=pci=noaer`
- remove args: `sudo grubby --update-kernel=ALL --remove-args=pci`
