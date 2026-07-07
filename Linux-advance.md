# SSH (Secure Shell)
```
exit : to logout server
```
## What is SSH?

**SSH (Secure Shell)** is a secure way to connect to another computer over a network and control it using the command line.

It creates an **encrypted connection**, which keeps your data safe from hackers while communicating with the remote machine.

---

## Simple Explanation

Think of SSH as a **secure tunnel** between your computer and another computer.

Instead of sitting in front of the remote computer, you can access and control it from anywhere.

---

## Why Do We Use SSH?

- Securely connect to remote Linux servers.
- Run commands on another computer.
- Manage cloud servers (AWS, Azure, GCP).
- Transfer files securely.
- Protect data using encryption.

---

# Understanding the SSH Command

```bash
ssh -i "om-key.pem" ubuntu@ec2-54-257-247-191.compute-1.amazonaws.com
```

Let's break it down piece by piece.

---

## `ssh`

- Stands for **Secure Shell**.
- It is the command used to securely connect to a remote Linux server.

```bash
ssh
```

Means: "I want to start an SSH connection."

---

## `-i`

- `-i` stands for **Identity File**.
- It tells SSH which **private key** to use for authentication.

```bash
-i "om-key.pem"
```

Means:

> "Use the private key named `om-key.pem` to prove my identity."

---

## `"om-key.pem"`

This is your **private key file**.

Example:

```text
Downloads/
└── om-key.pem
```

- You downloaded this file when creating the EC2 instance.
- It stays only on your computer.
- Never share it with anyone.

---

## `ubuntu`

This is the **username** on the remote EC2 instance.

```bash
ubuntu@
```

Means:

> "Log in as the user named `ubuntu`."

Different Linux images use different default usernames:

| AMI | Default Username |
|------|------------------|
| Ubuntu | `ubuntu` |
| Amazon Linux | `ec2-user` |
| RHEL | `ec2-user` |
| Debian | `admin` or `debian` |
| CentOS | `centos` |

---

## `ec2-54-257-247-191.compute-1.amazonaws.com`

This is the **public DNS name** of your EC2 instance.

It points to your server on the internet.

Example:

```text
ec2-54-237-247-191.compute-1.amazonaws.com
```

Instead of the DNS name, you could also use the instance's public IP address, for example:

```bash
ssh -i test-key.pem ubuntu@54.237.247.191
```

Both connect to the same EC2 instance.

---

# Complete Flow

```text
ssh
 │
 │
 ├── -i
 │      │
 │      └── test-key.pem (Private Key)
 │
 ├── ubuntu
 │      │
 │      └── Username on the EC2 instance
 │
 └── ec2-54-237-247-191.compute-1.amazonaws.com
        │
        └── Public DNS of the EC2 instance
```


---

## Simple Meaning

Means:

> **"Use my private key (`om-key.pem`) to securely log in as the `ubuntu` user on the EC2 server identified by `ec2-54-257-247-191.compute-1.amazonaws.com`."**
> 
### Check SSH version

```bash
ssh -V
```

---

## What are Public and Private Keys?

Public and Private Keys are a pair of cryptographic keys used for **secure authentication** in SSH.

- **Public Key** → Can be shared with anyone.
- **Private Key** → Must be kept secret and never shared.

They work together to verify your identity without sending your password over the network.

---

## Simple Explanation

Imagine a **locked mailbox**.

- 📬 **Public Key** = The mailbox (anyone can use it).
- 🔑 **Private Key** = The only key that can open the mailbox (only you have it).

Anyone can put a letter into the mailbox using the public key, but only the person with the private key can open and read it.

---

AWS generates:

- Private Key 🔑 → Downloaded to your computer (`my-key.pem`)
- Public Key 📄 → Automatically stored on the EC2 instance
---

## Visual Representation

```text
Your Computer                          Remote Server

Private Key 🔑   -------------------->  (Never Shared)

Public Key 📄   -------------------->  Stored in ~/.ssh/authorized_keys

                SSH Login Request

Server verifies that the Private Key
matches the stored Public Key.

✔ Access Granted
```

---

## Why Use SSH Keys Instead of Passwords?

- More secure than passwords.
- Faster login.
- Harder for attackers to guess or steal.
- Commonly used in DevOps and Cloud environments.

## What is `authorized_keys`?

`authorized_keys` is a file on the **remote Linux server** that stores the **public keys** of users who are allowed to log in via SSH.

When you try to connect, SSH checks this file to verify whether your public key is authorized.


---

# Common Linux Commands

| Command                        | Description                                                                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `exit`                         | Logs out of the current SSH session.                                                                                                             |
| `cat /etc/ssh/sshd_config`     | Displays the SSH server (`sshd`) configuration file.                                                                                             |
| `sudo apt install nginx`       | Installs the Nginx web server.                                                                                                                   |
| `systemctl status nginx`       | Checks the current status of the Nginx service.                                                                                                  |
| `sudo systemctl start nginx`   | Starts the Nginx service.                                                                                                                        |
| `sudo systemctl stop nginx`    | Stops the Nginx service.                                                                                                                         |
| `sudo systemctl restart nginx` | Restarts the Nginx service.                                                                                                                      |
| `journalctl -u nginx`          | Displays logs for the Nginx service.                                                                                                             |
| `journalctl -u nginx -f`       | Displays live (real-time) logs for the Nginx service.                                                                                            |
| `sudo apt update`              | Downloads the latest package information from the repositories. It updates the local package index but does **not** install or upgrade packages. |
| `sudo apt upgrade`             | Upgrades installed packages to their latest available versions using the updated package index.                                                  |


### User management

# Linux User Management Commands

| Command                  | Description                                                                      |
| ------------------------ | -------------------------------------------------------------------------------- |
| `sudo useradd -m berlin` | Creates a new user named **berlin** with a home directory (`/home/berlin`).      |
| `sudo`                   | Executes the command with administrator (root) privileges.                       |
| `useradd`                | Creates a new Linux user account.                                                |
| `-m`                     | Automatically creates a home directory for the new user.                         |
| `berlin`                 | The username of the new user.                                                    |
| `sudo passwd berlin`     | Sets or changes the password for the **berlin** user.                            |
| `su berlin`              | Switches to the **berlin** user.                                                 |
| `su - berlin`            | Switches to the **berlin** user and loads their login environment (recommended). |
| `whoami`                 | Displays the username of the currently logged-in user.                           |
| `id berlin`              | Displays the UID, GID, and group information of the **berlin** user.             |
| `sudo useradd -m tokyo -s /usr/bin/bash ` | cretaes new user without black terminal             |


## Grouping
```
sudo usermod -aG <group_name> <username>
```
| Part         | Meaning                                                                                 |
| ------------ | --------------------------------------------------------------------------------------- |
| `sudo`       | Run the command with administrator (root) privileges.                                   |
| `usermod`    | Modify an existing user account.                                                        |
| `-a`         | **Append** the user to the new group(s) without removing existing supplementary groups. |
| `-G`         | Specify the **supplementary (secondary) group(s)** to assign.                           |
| `<group_name>` | The group to add the user to.                                                           |
| `<username>`     | The username to modify.                                                                 |

| Command                                 | Purpose                                           |
| --------------------------------------- | ------------------------------------------------- |
| `sudo gpasswd -a <username> <group>`    | Add a user to a group.                            |
| `sudo gpasswd -d <username> <group>`    | Remove a user from a group.                       |
| `sudo gpasswd -A <user1,user2> <group>` | Assign group administrator(s).                    |
| `sudo gpasswd -M <user1,user2> <group>` | Replace the group's member list.                  |
| `sudo gpasswd -r <group>`               | Remove the group's password.                      |
| `sudo gpasswd <group>`                  | Set or change the group's password (rarely used). |
| ` newgrp docker`                  |refresh the service |

```
Why use a group?

Suppose there's a project folder:

/project

Instead of giving permissions like this:

Give Berlin access ✅
Give Tokyo access ✅
Give Mumbai access ✅

you simply make the folder belong to the devops group:

Owner : root
Group : devops

Now everyone in the devops group can access the folder according to the group's permissions.
```
```
chown stands for Change Owner.

