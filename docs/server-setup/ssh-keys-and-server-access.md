# SSH Keys and Server Access

## What are SSH Keys?

SSH keys are a secure way to log in to another computer or server without using a password. Instead, you use a pair of cryptographic keys:

- **Private Key:** Stored safely on your computer (never shared).
- **Public Key:** Shared with the remote machine (placed in `~/.ssh/authorized_keys`).

Think of the public key as a lock and the private key as the only key that opens it.

---

## How SSH Access Works

1. **Generate a key pair on your system:**

   ```bash
   ssh-keygen
   ```

   This creates:

   - `id_rsa` → Your private key (keep this safe)
   - `id_rsa.pub` → Your public key (you can share this)

2. **Copy your public key to the remote system:**

   ```bash
   # On the remote machine, add your public key to:
   ~/.ssh/authorized_keys
   ```

3. **SSH into the remote machine:**

   ```bash
   ssh username@ip_address
   ```

---

## How to Find Someone’s IP (Example Idea)

You can serve a local website using:

```bash
   npx serve
```

Ask the person to open the link. When they visit it, you’ll capture their IP — which you can then use to attempt SSH (if their system is configured to allow it).

## Example: DigitalOcean Droplet

If you created a Droplet (virtual server) on DigitalOcean with SSH access:

```bash
ssh root@your_droplet_ip
```

Your public key will be in:

```bash
~/.ssh/authorized_keys
```

To check:

```bash
cd ~/.ssh
cat authorized_keys
```

---

## Real-World Example: GitHub

- Add your public key to your GitHub account.
- When you `git clone` a private repo, GitHub checks if your private key matches the stored public key.
- If yes, access is granted — no password needed!

---

## Virtual Machines (Cloud Servers)

Platforms like:

- **DigitalOcean:** Droplets
- **AWS:** EC2 Instances

...are just virtual Linux machines in the cloud. You can log into them via SSH using the steps above.
