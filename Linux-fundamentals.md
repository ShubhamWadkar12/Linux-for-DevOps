# Linux-for-DevOps

Notes : https://app.eraser.io/workspace/1QwekzTJC2FJAoRmYL1M

### What is Linux?

Linux is an open-source operating system that manages your computer's hardware and software.

Just like Windows and macOS, Linux is an operating system.

Operating System = Bridge between User and Hardware

You
   ↓
Operating System (Linux)
   ↓
CPU • RAM • Hard Disk • Network

Linux tells the hardware what to do when you run commands or applications.

### What is the Linux Kernel?

The Kernel is the heart (core) of Linux.

It directly communicates with the hardware.

Without the kernel, Linux cannot work.

Applications
      ↓
Shell
      ↓
Linux Kernel
      ↓
Hardware
The kernel manages
CPU
Memory (RAM)
Hard Disk
USB Devices
Keyboard
Mouse
Network

Think of the kernel as the manager of a company. Every request goes through the manager before reaching employees (hardware).

### What is GNU/Linux?

Linux originally contained only the Kernel.

To make a complete operating system, developers added GNU tools like:

Bash Shell
ls
cp
mv
cat
gcc
Libraries
Linux Kernel
       +
GNU Tools
       =
GNU/Linux

Today, when people say "Linux", they usually mean GNU/Linux.

### What are Linux Distributions?

A Linux Distribution (Distro) is a ready-to-use operating system made using the Linux kernel.

Linux Kernel
      +
Software
      +
Package Manager
      +
Desktop (optional)
      =
Linux Distribution
Popular Linux Distributions
Ubuntu
Beginner friendly
Most popular
Great for learning DevOps

Used by:

Students
Startups
Cloud Servers
RHEL (Red Hat Enterprise Linux)
Enterprise Linux
Paid version
Used by large companies

Used in:

Banks
IT Companies
Government
CentOS
Free version based on RHEL
Stable
Earlier widely used for servers
Rocky Linux
Successor to CentOS
Free
Enterprise-grade
Debian
Very stable
Lightweight
Parent of Ubuntu
Amazon Linux
Created by AWS
Optimized for EC2 instances
Commonly used in cloud environments

### Why Linux Dominates Servers

Around 90%+ of cloud servers run Linux because it is:

Free to use
Fast
Secure
Stable
Uses fewer resources
Highly customizable
Easy to automate
Excellent for networking

Imagine two computers with the same hardware:

Windows Server may use more RAM and CPU for its graphical interface.
Linux can run with minimal resources because it often runs without a GUI.

That makes Linux ideal for servers.

### Why DevOps Engineers Use Linux

Almost every DevOps tool runs on Linux.

Examples:

Docker
Kubernetes
Jenkins
Ansible
Terraform
Nginx
Apache

### Linux File System

Linux stores everything inside one main directory called the Root Directory (/).

Think of it like the trunk of a tree, with all other directories branching from it.

## Linux File System Structure

```text
/
├── bin      # Essential user commands
├── boot     # Boot loader files
├── dev      # Device files
├── etc      # System configuration files
├── home     # User home directories
├── lib      # Shared libraries
├── media    # Mounted removable devices
├── mnt      # Temporary mount point
├── opt      # Optional third-party software
├── proc     # Process and kernel information
├── root     # Root user's home directory
├── run      # Runtime data
├── sbin     # System administration commands
├── srv      # Service data
├── sys      # System and hardware information
├── tmp      # Temporary files
├── usr      # User applications and libraries
└── var      # Logs, cache, and variable data
```
________
<img width="702" height="522" alt="image" src="https://github.com/user-attachments/assets/25b382ac-dae4-4873-a61a-8e9995f74ea2" />


| Command   | Use (4–5 words)                   |
| --------- | --------------------------------- |
| `pwd`     | Show current directory path       |
| `ls`      | List files and directories        |
| `cd`      | Change current directory          |
| `mkdir`   | Create a new directory            |
| `mkdir -p josh/batch10/files`   | Create  directory under directory|
| `rmdir`   | Remove empty directory            |
| `touch`   | Create empty file                 |
| `cp`      | Copy files or directories         |
| `mv`      | Move or rename files              |
| `rm`      | Delete files or directories       |
| `cat`     | Display file contents             |
| `less`    | View file page by page            |
| `more`    | View file one page                |
| `head`    | Show first few lines              |
| `tail`    | Show last few lines               |
| `echo`    | Print text or variables           |
| `clear`   | Clear terminal screen             |
| `history` | Show previously executed commands |
| ` cd /usr/bin + ls ` | To see all linux commands |

_______

### Linux Boot Process

```text
                 +----------------+
                 |   Power On     |
                 +----------------+
                          │
                          ▼
                 +----------------+
                 |  BIOS / UEFI   |
                 | Hardware Check |
                 |     (POST)     |
                 +----------------+
                          │
                          ▼
                 +----------------+
                 | GRUB Bootloader|
                 +----------------+
                          │
                          ▼
                 +----------------+
                 | Linux Kernel   |
                 +----------------+
                          │
                          ▼
                 +----------------+
                 | systemd (PID 1)|
                 |  Init Process  |
                 +----------------+
                          │
          ┌───────────────┼────────────────┐
          ▼               ▼                ▼
   +-------------+  +-------------+  +-------------+
   | Docker      |  | SSH         |  | Nginx       |
   | Service     |  | Service     |  | Service     |
   +-------------+  +-------------+  +-------------+
          │
          ▼
                 +------------------------+
                 | Login Screen / Shell   |
                 +------------------------+
```

### Common Linux Process States

| State | Meaning               | Description                                                   |
| ----- | --------------------- | ------------------------------------------------------------- |
| **R** | Running               | Process is running or ready to run on the CPU.                |
| **S** | Sleeping              | Waiting for an event (most common state).                     |
| **D** | Uninterruptible Sleep | Waiting for I/O (disk, network, etc.). Cannot be interrupted. |
| **T** | Stopped               | Process has been paused.                                      |
| **Z** | Zombie                | Process has finished but its entry still exists.              |
| **I** | Idle                  | Idle kernel thread (common on modern Linux).                  |
