![system design preview](./../images/git-submodule-error.png)

### You Probably Did Something Like:

- Copied a folder that already had `.git` inside
- OR ran `git init` inside Docs before adding it

So Git thinks: “This is a separate repository inside your repo”

### How to Confirm

Run inside your repo:

```bash
git ls-files --stage
```

If you see something like:

```
160000 Docs
```

That confirms it’s a submodule

### What is a Submodule (Simple)?

A submodule = “A repo inside another repo”

- Git doesn’t store its files directly
- It only stores a reference (pointer) → that’s why the arrow icon (as shown in the figure)

### Why This is NOT What You Want

- Files inside Docs won’t behave like normal files 
- Others cloning your repo won’t get contents automatically 
- Push/pull becomes confusing 

### Fix (Convert to Normal Folder)

**Step 1: Remove submodule tracking**

```bash
git rm --cached Docs
```

**Step 2: Delete internal .git folder**

```bash
rm -rf Docs/.git
```

**Step 3: Add it again as normal folder**

```bash
git add Docs
git commit -m "Fix: convert Docs from submodule to normal folder"
git push
```

If such a problem arises (as shown in the figure with the arrow), follow these steps to resolve it easily.