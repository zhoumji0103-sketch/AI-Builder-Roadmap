# Setup Personal GitHub on an Enterprise Laptop

## Background

I use two GitHub accounts.

- Company GitHub
- Personal GitHub

The goal is to completely isolate company projects from personal open-source projects.

---

# Part 1 Install Git

Install Git for Windows.

Configure Git globally.

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

These configurations define the author information for future commits.

---

# Part 2 Initialize Repository

Create a project directory.

Initialize Git.

```bash
git init
```

Git creates a hidden `.git` directory.

It stores:

- Commit history
- Objects
- References
- Branches
- Repository configuration

Rename the default branch.

```bash
git branch -M main
```

Modern repositories generally use `main` as the default branch.

---

# Part 3 First Commit

Stage files.

```bash
git add .
```

Create a commit.

```bash
git commit -m "Initial commit"
```

Connect the local repository with GitHub.

```bash
git remote add origin <repository-url>
```

Check the remote.

```bash
git remote -v
```

Push for the first time.

```bash
git push -u origin main
```

The `-u` option sets the upstream branch so future pushes only require:

```bash
git push
```

---

# Part 4 HTTPS Authentication

Initially the repository used HTTPS.

```
Git
↓

Git Credential Manager

↓

Browser Login

↓

GitHub OAuth

↓

Push
```

On my enterprise laptop, Git Credential Manager automatically authenticated with the company GitHub account.

As a result, authentication to my personal GitHub repository failed.

---

# Part 5 SSH Authentication

I switched to SSH authentication.

First check existing SSH keys.

```bash
ls ~/.ssh
```

Generate a dedicated SSH key for my personal GitHub account.

```bash
ssh-keygen -t ed25519 -C "zhoumji0103@gmail.com" -f ~/.ssh/id_ed25519_personal
```

Upload the public key (`.pub`) to GitHub.

The private key always stays on the local machine.

---

# Part 6 Why Did SSH Still Fail?

The push still failed.

```
Permission denied to xxx
```

Although a new SSH key existed, SSH authenticated using the default company key first.

Once GitHub accepted that identity, SSH stopped trying other keys.

---

# Part 7 SSH Config

Create a dedicated SSH host.

```text
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes
```

Update the Git remote.

```bash
git remote set-url origin git@github-personal:zhoumji0103-sketch/AI-Builder-Roadmap.git
```

Test the SSH connection.

```bash
ssh -T git@github-personal
```

After successful authentication:

```bash
git push
```

worked correctly.

---

# Reflection

Today I learned much more than Git commands.

I understood:

- Difference between HTTPS and SSH authentication
- Public key vs private key
- Why GitHub stores only the public key
- How SSH selects an identity
- How SSH config isolates multiple GitHub accounts

This is the first step toward understanding software engineering rather than simply memorizing Git commands.