---
title: Creating a bootable USB flash drive from an ISO file 
description: In this article we'll learn to write ISOs to USB drives easily using ddgui. 
date: '2024-11-19'
categories:
  - ddgui
  - linux
  - rust
published: true
---

<script lang="ts">
    const screenshot: string = "https://raw.githubusercontent.com/miguelnto/ddgui/refs/heads/main/doc/screenshot.png";
    import screenshot2 from "$lib/images/screenshot_2.png";
    const ddgui_logo: string = "https://raw.githubusercontent.com/miguelnto/ddgui/main/doc/ddgui_logo.png"
</script>

<img style="margin: auto;" width="200" src={ddgui_logo} alt="me" />

If you want to test out new Linux distros or just install a new OS on another computer, you'll often have to create a bootable USB drive with an ISO image of the system. In this article we'll learn to write ISOs to USB drives using **ddgui**, a GUI frontend for `dd`.

## Dependencies

`ddgui` depends on Rust and cargo. On an Arch based distribution (such as Manjaro, Arch Linux), you can install them using Pacman:

```
sudo pacman -S rust
```

This will install the `rustc` compiler and [Cargo](https://wiki.archlinux.org/title/Rust#Cargo).

## Installing

First, let's clone the repository and go the `ddgui` directory:

```
git clone https://github.com/miguelnto/ddgui
cd ddgui
```

Now let's compile and install the program:

```
sudo make install
```

## Usage

Invoke the program from the command line as root:

```
sudo ddgui
```

When you open the program, you should see something like this:

<img width="1200" src={screenshot} alt="me" />

Select the ISO and the device where you want to write the ISO, then click **Start**.

<img width="1200" src={screenshot2} alt="me" />

After the process is finished, if no error occurs, it will show "Process finished sucessfully" on the screen. The USB drive is now bootable and you can proceed booting into the system.

**Happy hacking!**

*If this article has helped you in any way, consider [supporting](support) this blog. Feel free to [contact me](contact) as well.*

