# Setting Up Multiple Git Accounts

## Step 1: Create SSH Keys

If `.ssh` directory is not present, check with `ls -a` and create it:

```bash
mkdir -p ~/.ssh
```

Generate the first SSH key for your personal account:

```bash
ssh-keygen -t ed25519 -C "personal-email@example.com"
```

When prompted for the file in which to save the key, type the full path:

Save as:

```
~/.ssh/id_ed25519_personal
```

Verify with:

```bash
ls ~/.ssh
```

You should see:

- `id_ed25519_personal`
- `id_ed25519_personal.pub`

Now generate the second SSH key for your work account:

```bash
ssh-keygen -t ed25519 -C "work-email@example.com"
```

Save as:

```
~/.ssh/id_ed25519_work
```

If you set a passphrase (for securing the keys), start the SSH agent to bind the terminal to the credentials:

```bash
eval "$(ssh-agent -s)"
```

## Step 2: Add Keys to SSH Agent

```bash
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

## Step 3: Add Keys to GitHub

Copy the public keys:

```bash
pbcopy < ~/.ssh/id_ed25519_personal.pub
```

Or display them:

```bash
cat ~/.ssh/id_ed25519_personal.pub
cat ~/.ssh/id_ed25519_work.pub
```

Add each key to the respective GitHub account:
- Go to GitHub → Settings → SSH and GPG Keys → New SSH Key (as Authentication Key)

## Step 4: Configure SSH (Very Important)

Edit the SSH config file:

```
~/.ssh/config
```

Open it with:

```bash
nano ~/.ssh/config
```

Add the following:

```
# Personal
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal

# Work
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work

# Default
Host github
    HostName github.com
    User git
    IdentityFile ~/.ssh/current_github_key
```

Save and exit:

- Ctrl + X

- Y

- Enter

## Step 5: Test the SSH Connections

Test the personal account:

```bash
ssh -T git@github-personal
```

Expected output:

```
Hi <username>! You've successfully authenticated
```

Test the work account:

```bash
ssh -T git@github-work
```

Expected output:

```
Hi <username>! You've successfully authenticated
```

## Step 6: Create Smart Git Aliases

These aliases switch your Git identity and remote URL for each account.

```bash
git config --global alias.use-personal '!f() { git config user.name "your-name"; git config user.email "your-personal-email"; url=$(git remote get-url origin); url=${url/github.com/github-personal}; url=${url/github-work/github-personal}; git remote set-url origin $url; }; f'
```

```bash
git config --global alias.use-work '!f() { git config user.name "your-name"; git config user.email "your-work-email"; url=$(git remote get-url origin); url=${url/github.com/github-work}; url=${url/github-personal/github-work}; git remote set-url origin $url; }; f'
```

Create switch commands (global)

[OPTIONAL - ONE CAN SKIP THIS SWITCH COMMANDS IF IN DEFAULT CASE IN STEP 4 IDENTITY FILE IS SET TO PERSONAL OR WORK ONE]

```bash
git config --global alias.ssh-personal '!ln -sf ~/.ssh/id_ed25519_personal ~/.ssh/current_github_key'
```

```bash
git config --global alias.ssh-work '!ln -sf ~/.ssh/id_ed25519_work ~/.ssh/current_github_key'
```

## Step 7: Now before doing anything on github switch to the correct intented github account

[FOR DEFAULT CASE]

Switch to personal account in a repository:

```bash
git ssh-personal
```

Switch to work account:

```bash
git ssh-work
```

check which account is correctly default is pointing

```bash
ssh -T git@github.com
```

--- 
### Second method - [TO BE USED IN GIT INITIALISED REPO]

Switch to personal one:

```bash
git use-personal
```

Switch to work account:

```bash
git use-work
```
---

Check your current Git identity (used for commits):

```bash
git config user.name
git config user.email
```

Verify the remote URL anytime:

```bash
git remote -v
```

It should show something like:

```
origin  git@github-personal:...
```

---- 

**Note:**
- `git ssh-personal` / `git ssh-work`: Switch the default SSH key before cloning a repository
- `git use-personal` / `git use-work`: Switch Git identity and remote URL within an already initialized repository
- `git remote -v`: Verify which account the current repository is configured with
