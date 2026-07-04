# SSH (Secure Shell)

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


