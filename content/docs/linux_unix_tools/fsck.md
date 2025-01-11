+++
title = 'fsck'
date = 2024-12-16T00:40:15+05:30
draft = false
description = "Information on fsck command"
+++

- Used to check file systems for errors and repair them if possible
- fsck is a wrapper tool for efsck (ext) and e2fsck (ext2, dosfsck, fsckvfat)
- If error is found and if fsck tool able to fix it then it will promt option for your permission to proceed for fix or not.
    - example: fix inodes corruption

- `fsck /dev/blockdeviceid`
    - example: `fsck /dev/sda1`

- for getting block device list use: `lsblk` and `fdisk -l` with root privilages
