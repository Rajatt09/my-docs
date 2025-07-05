# SSH Keys and Server Access

## What are SSH Keys?

SSH keys are a secure way to log in to another computer or server without using a password. Instead, you use a pair of cryptographic keys:

- **Private Key:** Stored safely on your computer (never shared).
- **Public Key:** Shared with the remote machine (placed in `~/.ssh/authorized_keys`).

Think of the public key as a lock and the private key as the only key that opens it.

---

## How SSH Access Works

(a) **Generate a key pair on your system:**

```bash
ssh-keygen
```

This creates:

- `id_rsa` → Your private key (keep this safe)
- `id_rsa.pub` → Your public key (you can share this)

**These above keys are stored in :**

- `C:\Users\<YourUsername>\.ssh` (on windows)
- `~/.ssh/` (on linux)

You can run following cmd:

- `ls -la ~/.ssh` (lists all files, including hidden ones with detailed info like file permissions, etc)
- `cat ~/.ssh/id_ed25519.pub` (To view your public key (example for Ed25519):)

---

**Copy your public key to the remote system:**

```bash
# On the remote machine, add your public key to:
~/.ssh/authorized_keys
```

---

(b) **SSH into the remote machine:**

(i) `Enable OpenSSH Server on the Windows machine.`
[ Go to Settings > Apps > Optional Features ]

- If OpenSSH Server is not installed, click Add a feature and install OpenSSH Server

- Then start it:

```bash
  Start-Service sshd
  Set-Service -Name sshd -StartupType 'Automatic'
```

(ii) `Now create authorized_keys file in .ssh folder`

```bash
echo your-public-key >> ~/.ssh/authorized_keys #(for linux)

notepad C:\Users\<RemoteUsername>\.ssh\authorized_keys #(for windows)
```

---

Put the authorized_keys file in either of:

- C:\Users\<RemoteUsername>\.ssh\authorized_keys (user-level login)

- C:\ProgramData\ssh\administrators_authorized_keys (for admin-level access)

---

(iii) `Make sure the .ssh folder and authorized_keys file have the right permissions:`

```bash
icacls C:\Users\<RemoteUsername>\.ssh /grant <RemoteUsername>:"(R,W)"
```

(iv) `Restart-Service sshd (optional) :`

```bash
Restart-Service sshd  # optional
```

---

(v) `SSH into the Windows machine (from your local machine)`

```bash
ssh username@windows-remote-ip
```

---

## How to Find Someone’s IP (Example Idea)

You can serve a local website using:

```bash
   npx serve
```

Ask the person to open the link. When they visit it, you’ll capture their IP — which you can then use to attempt SSH (if their system is configured to allow it).

---

## Examples

### DigitalOcean Droplet

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

### EC2 Instance (AWS)

While setting up a server on aws you can create the ssh key-pair for a particular user and then can download it and

(i) Run this command (if you have choosen ubuntu machine)

```bash
ssh -i rajat.pem ubuntu@ip_address
```

**where this - i : input keypair rajat.pem which should be in root folder i.e. /users/<username> ,otherwise it will pick the default key-pair stored in ~/.ssh**

(ii) Change rajat.pem file access mode (permissions)

- Check the permission of file using:

```bash
ls -al #(for bash)
ls -Force #(for windows)
```

- Run below command to change permissions:

```bash
chmod 700 rajat.pem
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
