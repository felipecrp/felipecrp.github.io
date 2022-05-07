---
layout: post
title: How to install Arch Linux on WSL and create the perfect develop environment on Windows
comments: true
excerpt_separator: <!--more-->
---

## How to check the image integrity?

After downloading the image file from the official mirror, it is important to verify the file integrity to confirm that the correct file was downloaded and is not corrupted. It is possible to check the file integrity verifying the SHA-256 hash sum, i.e., calculate the file hash with the SHA-256 algorithm and compare the result with the provided value. The `sha256sum` command can calculate the SHA-256 hash sum and can verify if the file match the provided hash. The following command show how to verify the file using the `sha256sum`.   

```bash
$ sha256sum -c sha256sums.txt
``` 

The results ...

```text
sha256sum: archlinux-2022.05.01-x86_64.iso: No such file or directory
archlinux-2022.05.01-x86_64.iso: FAILED open or read
**archlinux-bootstrap-2022.05.01-x86_64.tar.gz: OK**
sha256sum: WARNING: 1 listed file could not be read
```
teste