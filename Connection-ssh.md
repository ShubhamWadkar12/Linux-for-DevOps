# Technical Explanation of SSH Key-Based Authentication Between Two EC2 Instances

## Scenario

I had two EC2 instances:

- **Instance 1:** `test`
- **Instance 2:** `dummy-server`

Each instance was initially created with a different AWS EC2 key pair.

---

## Step 1: Connect to the `test` Instance

From my local machine, I connected to the `test` instance using the AWS-generated private key.

```bash
ssh -i test-key.pem ubuntu@<test-public-ip>
```

This authenticated me to the `test` instance using the AWS key pair.

---

## Step 2: Generate a New SSH Key Pair

Inside the `test` instance, I generated a new SSH key pair.

```bash
ssh-keygen
```

This created:

```text
~/.ssh/id_ed25519        ← Private Key
~/.ssh/id_ed25519.pub    ← Public Key
```

*(Or `id_rsa` and `id_rsa.pub` if RSA was selected.)*

---

## Step 3: Copy the Public Key

I displayed the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

The output looked similar to:

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI...
```

This is the public key that can be safely shared.

---

## Step 4: Authorize the Key on `dummy-server`

I connected to the `dummy-server` using the AWS browser terminal.

Then I opened:

```bash
vim ~/.ssh/authorized_keys
```

and pasted the public key from the `test` instance into this file.

The `authorized_keys` file stores the public keys that are permitted to authenticate to the server.

---

## Step 5: SSH from `test` to `dummy-server`

From the `test` instance, I initiated an SSH connection.

```bash
ssh ubuntu@<dummy-server-public-ip>
```

or

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@<dummy-server-public-ip>
```

SSH used the private key (`id_ed25519`) stored on the `test` instance.

---

## Authentication Process

1. The SSH client on `test` initiated a connection to `dummy-server`.
2. `dummy-server` looked for matching public keys in:

```bash
~/.ssh/authorized_keys
```

3. The server sent a cryptographic challenge.
4. The SSH client signed the challenge using the private key (`id_ed25519`).
5. `dummy-server` verified the signature using the corresponding public key stored in `authorized_keys`.
6. Since the keys matched, authentication succeeded.
7. SSH established an encrypted session.
