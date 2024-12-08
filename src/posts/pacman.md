---
title: The basics of Pacman on Arch Linux
description: In this article we'll learn everything you need to know to effectively use Pacman on Arch Linux.
date: '2024-11-18'
categories:
  - arch linux
  - linux
  - package-manager
published: true
---

<script lang="ts">
    const arch: string = "https://archlinux.org/static/logos/archlinux-logo-dark-90dpi.ebdee92a15b3.png";
</script>

<br>

<img style="margin: auto;" width="450" src={arch} alt="me" />

###  Introduction

Pacman is the official Arch Linux package manager (which of course is used in other Arch based distros, such as Manjaro). It features dependency support, package groups, install and uninstall scripts, etc. You can read all the details on the **man page** for Pacman. 

In this article we'll explore everything you need to know about package management on an Arch-Based distribution, through examples.

#### Installing and uninstalling packages

To install a package, run `pacman -S <package-name>` (as root, of course). If I wanted to install vim, for example, I can run:

```
sudo pacman -S vim
```

This will install vim and all the packages it depends on. Now, if you want to uninstall a program, for example vim, run:

```
sudo pacman -Rns vim
```

This will remove vim, all of its dependencies, and all of its system configuration files.

#### Updating

To update all of your programs if they have new versions, run:

```
sudo pacman -Syu
```

This will update the package list and upgrade all packages afterwards. Here, `-S` means sync, `y` means synchronize package databases (without updating), and `u` means update. 

#### Searching for a package

If you want to search for a program, let's say vim, run the following command:

```
pacman -Ss vim
```

This is going to search for names or descriptions that has 'vim' on it.

#### Listing packages

To list out all of the packages installed on your system:

```
pacman -Q
```

To list the programs that you explicitly installed, without its dependencies:

```
pacman -Qe
```

To list out all of the packages installed on your system, but show only the names of the programs:

```
pacman -Qeq
```

To list only programs installed from the main repository:

```
pacman -Qn
```

To list only programs installed from the AUR:

```
pacman -Qm
```

To list all unneeded dependencies:

```
pacman -Qdt
```

#### Cleaning up packages

To remove all the unnecessary packages from the cache and remove unused repositories:

```
sudo pacman -Sc
```
#### Conclusion

Mastering the Pacman package manager is an essential skill for any Arch Linux user. With Pacman, you can easily manage your system's software, install new packages, and keep your system up to date. By following the steps outlined in this article, you should now have a basic understanding of how to use Pacman to manage your Arch Linux system. 

**Happy hacking!**

*If this article has helped you in any way, consider [supporting](support) this blog. Feel free to [contact me](contact) as well.*

