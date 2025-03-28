---
layout: post
title: How to install Arch Linux on WSL and create the perfect develop environment on Windows
comments: true
excerpt_separator: <!--more-->
---

## Introduction

Windows Subsystem for Linux (WSL) enables developers to run a Linux distribution
inside Windows. The WSL is pretty optimized and provides a great development
environment. It is a joint project from Microsoft and Canonical and its default
Linux distribution is Ubuntu.

The WSL users can install Ubuntu direct from the Microsoft App Store. However,
the Microsoft App Store does not provide Arch Linux. Hence, users that want to
run Arch Linux over WSL need to install it manually.

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

## Let's create our Arch Linux WSL image

Unfortunately, Microsoft does not provide an Arch Linux for WSL in the App
Store. Hence, we need to build the image.

##



### How to check the image integrity?

After downloading the image file from the officigl mirror, it is important to
verify the file integrity to confirm that the correct file was downloaded and is
not corrupted. It is possible to check the file integrity verifying the SHA-256
hash sum, i.e., calculate the file hash with the SHA-256 algorithm and compare
the result with the provided value. The `sha256sum` command can calculate the
SHA-256 hash sum and can verify if the file match the provided hash. The
following command show how to verify the file using the `sha256sum`.   

```bash $ sha256sum -c sha256sums.txt ``` 

The results ...

```text sha256sum: archlinux-2022.05.01-x86_64.iso: No such file or directory
archlinux-2022.05.01-x86_64.iso: FAILED open or read
**archlinux-bootstrap-2022.05.01-x86_64.tar.gz: OK** sha256sum: WARNING: 1
listed file could not be read ```

1. Download archbootstrap

2. Remove rootfs folder - no WSL copiar para um WSL sudo tar xzf
   archlinux-bootstrap-2022.05.01-x86_64.tar.gz  --numeric-owner cd root.x86_64
   sudo vim etc/pacman.d/mirrorlist
 - Habilitar um mirror
sudo tar czf ../archlinux-bootstrap.tar.gz  .

3. Create the WSL wsl.exe --import arch "c:\users\felip\WSL\arch"
archlinux-bootstrap.tar.gz wsl.exe -d arch -u root

3. config user

useradd -m felipecrp passwd felipecrp New password: Retype new password: passwd:
password updated successfully usermod -aG wheel felipecrp

4. init pacman [root@cRP-Desktop ~]# pacman-key --init [root@cRP-Desktop ~]#
pacman-key --populate archlinux

pacman -Sy vi

vi /etc/wsl.conf [user] default=felipecrp

pacman -Sy sudo visudo

## Uncomment to allow members of group wheel to execute any command %wheel
ALL=(ALL:ALL) ALL


wsl.exe --terminate arch


# instalar o yay sudo pacman -S --needed git base-devel git clone
https://aur.archlinux.org/yay.git cd yay makepkg -si cd .. rm -rf yay

# Atualizar o sistema yay -Sy

Bonus: sudo vi /etc/pacman.conf

ParallelDownloads = 5

Bonus: yay -Sy ttf-font

# começar a usar

yay -Sy python python-pip r



-----------------------

R. yay -Sy python python-pip r yay -Sy libcurl4-opensslv libssl libxml2

pip install radian export PATH="$HOME/.local/bin:$PATH"

Bonus: colocar no .bash_profile ou .zshrc

install.packages("tidyverse") criar biblioteca local e escolhehr o mirror

O processo demora ...

se for usar o vscode. https://code.visualstudio.com/docs/languages/r
https://marketplace.visualstudio.com/items?itemName=REditorSupport.r
https://marketplace.visualstudio.com/items?itemName=RDebugger.r-debugger

install.packages(c("languageserver", "httpgd", "lintr"))

yay -Sy wget ca-certificates


--------------------------------

yay -Sy zsh oh-my-zsh-git [felipecrp@cRP-Desktop ~]$ chsh -l /bin/sh /bin/bash
/usr/bin/git-shell /bin/zsh /usr/bin/zsh

chsh felipecrp -s /bin/zsh cp /usr/share/oh-my-zsh/zshrc .zshrc



tmp mkdir -p $(wslpath -u "D:\Users\curty\wsl\arch") ➜  tmp wsl.exe --import
arch "D:\Users\curty\wsl\arch" archlinux-bootstrap.tar.gz


---

1. Download archbootstrap

2. Remove rootfs folder - no WSL

wget http://br.mirror.archlinux-br.org/iso/2022.05.01/sha256sums.txt wget
http://br.mirror.archlinux-br.org/iso/2022.05.01/archlinux-bootstrap-2022.05.01-x86_64.tar.gz

➜  tmp sha256sum -c sha256sums.txt sha256sum: archlinux-2022.05.01-x86_64.iso:
No such file or directory archlinux-2022.05.01-x86_64.iso: FAILED open or read
archlinux-bootstrap-2022.05.01-x86_64.tar.gz: OK sha256sum: WARNING: 1 listed
file could not be read



copiar para um WSL sudo tar xzf archlinux-bootstrap-2022.05.01-x86_64.tar.gz
--numeric-owner cd root.x86_64 sudo vim etc/pacman.d/mirrorlist
 - Habilitar um mirror
sudo tar czf ../archlinux-bootstrap.tar.gz  .

3. Create the WSL wsl.exe --import arch "c:\users\felip\WSL\arch"
archlinux-bootstrap.tar.gz wsl.exe -d arch -u root

3. config user

useradd -m felipecrp passwd felipecrp New password: Retype new password: passwd:
password updated successfully usermod -aG wheel felipecrp

4. init pacman [root@cRP-Desktop ~]# pacman-key --init [root@cRP-Desktop ~]#
pacman-key --populate archlinux

pacman -Sy vi

vi /etc/wsl.conf [user] default=felipecrp

pacman -Sy sudo visudo

## Uncomment to allow members of group wheel to execute any command %wheel
ALL=(ALL:ALL) ALL


wsl.exe --terminate arch


# instalar o yay sudo pacman -S --needed git base-devel git clone
https://aur.archlinux.org/yay.git cd yay makepkg -si cd .. rm -rf yay

# Atualizar o sistema yay -Sy

Bonus: sudo vi /etc/pacman.conf

ParallelDownloads = 5

Bonus: yay -Sy ttf-font

# começar a usar

yay -Sy python python-pip r



-----------------------

R. yay -Sy python python-pip r yay -Sy libcurl4-opensslv yay -Sy libssl yay -Sy
libxml2 yay -Sy ttf-font

pip install radian export PATH="$HOME/.local/bin:$PATH"

Bonus: colocar no .bash_profile ou .zshrc

install.packages("tidyverse") criar biblioteca local e escolhehr o mirror

O processo demora ...

se for usar o vscode. https://code.visualstudio.com/docs/languages/r
https://marketplace.visualstudio.com/items?itemName=REditorSupport.r
https://marketplace.visualstudio.com/items?itemName=RDebugger.r-debugger

install.packages(c("languageserver", "httpgd", "lintr"))

yay -Sy wget ca-certificates


--------------------------------

yay -Sy zsh oh-my-zsh-git [felipecrp@cRP-Desktop ~]$ chsh -l /bin/sh /bin/bash
/usr/bin/git-shell /bin/zsh /usr/bin/zsh

chsh felipecrp -s /bin/zsh cp /usr/share/oh-my-zsh/zshrc .zshrc
