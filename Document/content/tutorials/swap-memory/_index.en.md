---
title: Swap Memory
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

This tutorial instructs qitmeer node maintainers to mount swap memory to solve the Out of Memory problem.

## Problem Description
Qitmeer's recommended memory perquisite is 2GB, 1 GB at minimum. Even though memory has satisfied the recommended requirement, it is still possible that Qitmeer gets killed by system due to peak usage of memory, called Out of Memory exception.

```sh
2021-03-23|07:45:22.110 [INFO ] Processed 211 blocks in the last 10s (217 transactions, order 283091, 2020-09-27 15:05:08 +0800 CST) module=blkmanager
[1]    196072 killed     ./build/bin/qitmeer

```

You may confirm this exception by the command:

> Note: assume OS is Ubuntu

```sh
dmesg -T| grep -E -i -B100 'killed process'
```
If you find similar output as follows, then that maybe the case
```sh
[Tue Mar  9 11:34:26 2021] Out of memory: Killed process 140587 (qitmeer) total-vm:1403144kB,
anon-rss:675828kB, file-rss:0kB, shmem-rss:0kB, UID:1001 pgtables:1532kB oom_score_adj:0
```

## Solution
### What is Swap Memory
OS could transfer inactive memory into hard disk to make room for active processes, called memory swapping. Although this mechanism would reduce the overall performance of  machines due to high swapping cost between physical memory and virtual memory (hard disk), it brings stronger stability.

## How to mount swap memory
> Note: Ensure you have root permission

1. create folder for swap file

```bash
root@Qit:/home/tony$ cd /
root@Qit:/$ mkdir swap
root@Qit:/$ cd swap/
```

2.  create a 2GB swap file
```bash
root@Qit:/swap$ dd if=/dev/zero of=SWAPFILE bs=1024 count=2097152
2097152+0 records in
2097152+0 records out
2147483648 bytes (2.1 GB, 2.0 GiB) copied, 14.838 s, 145 MB/s
```

3. convert into swap format 
```sh
root@Qit:/swap$ mkswap SWAPFILE 2097152
mkswap: SWAPFILE: insecure permissions 0644, 0600 suggested.
Setting up swapspace version 1, size = 2 GiB (2147479552 bytes)
no label, UUID=06ee7e99-ab8f-4378-b0d0-3f5477bd1090
```

4. format swap file
```sh
root@Qit:/swap$ swapon SWAPFILE
swapon: /swap/SWAPFILE: insecure permissions 0644, 0600 suggested.
```
check swap file usage
```sh
root@Qit:/swap$ free
              total        used        free      shared  buff/cache   available
Mem:         980192      271480       63400        2676      645312      545572
Swap:       2097148           0     2097148
```
5. auto mount swap file on booting
```sh
root@Qit:~$ echo "/swap/SWAPFILE swap swap defaults 0 0" >> /etc/fstab
```