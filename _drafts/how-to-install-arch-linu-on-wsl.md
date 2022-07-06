---
layout: post
title: How to install Arch Linux on WSL and create the perfect develop environment on Windows
comments: true
excerpt_separator: <!--more-->
---

# Introduction

Windows Subsystem for Linux (WSL2) enables developers to run a Linux
distribution inside Windows. The version 2 is pretty optimized and provides a
great performance for a development workflow. The WSL is a joint project from
Microsoft and Canonical and the its default distribution is Ubuntu.

Ubuntu is a pretty nice desktop distribution with a great community and many
packages available for general use. However, to keep the latest version of those
packages, we generally need to install alternative repositories, called Personal
Package Archives (PPA). Sometimes it took some effort to find the right PPA to
install.

...

Arch Linux enables access to most Linux packages in its latest versions. That is
why Arch Linux is an amazing distribution for developers. It allows developers
to install almost everything without the need to worry about finding a specific
repository. 

## How to check the image integrity?

After downloading the image file from the official mirror, it is important to
verify the file integrity to confirm that the correct file was downloaded and is
not corrupted. It is possible to check the file integrity verifying the SHA-256
hash sum, i.e., calculate the file hash with the SHA-256 algorithm and compare
the result with the provided value. The `sha256sum` command can calculate the
SHA-256 hash sum and can verify if the file match the provided hash. The
following command show how to verify the file using the `sha256sum`.   

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
