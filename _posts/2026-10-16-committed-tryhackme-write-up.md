---
title: Committed — TryHackMe Write-Up
date: 2026-10-16 00:00:00 +0200
categories:
  - Write-ups
---

Just completed the "[Committed](https://tryhackme.com/room/committed)" room on TryHackMe — and it's a perfect reminder that **Git never forgets**.

[Category](https://img.shields.io/badge/Category-Forensics-orange)

[Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

[Room Badge](https://img.shields.io/badge/TryHackMe-Committed-blue)

---

## Room Overview

| **Room Name** | Committed |
| --- | --- |
| **Platform** | TryHackMe |
| **Category** | Forensics |
| **Difficulty** | Easy |
| **Tags** | Git, Forensics, Source Code Analysis |

---

## 1. Introduction

Ever heard the phrase "Git never forgets"? This room proves exactly that. The scenario presents us with a common yet dangerous mistake: a developer accidentally committed sensitive information to a Git repository, then tried to remove it. Our mission is to dig through the commit history and uncover what was meant to stay hidden.

As digital forensic investigators, we'll explore how Git's architecture preserves every change forever, making it a goldmine for uncovering secrets.

---

## 2. Environment Setup

Once the target machine is deployed, all challenge files are located at:

```bash
/home/ubuntu/commited
```

Everything runs locally on the TryHackMe AttackBox — no additional configuration required.

---

## 3. Step-by-Step Walkthrough

### Step 1: Initial Reconnaissance

First, let's navigate to the directory and examine its contents:

```bash
cd /home/ubuntu/commited
ls -la
```

**Output:**

```
total 20
drwxrwxr-x 3 ubuntu ubuntu 4096 Aug 31 20:34 .
drwxr-xr-x 5 ubuntu ubuntu 4096 Aug 31 20:34 ..
-rw-rw-r-- 1 ubuntu ubuntu  220 Aug 31 20:34 .bash_logout
-rw-rw-r-- 1 ubuntu ubuntu 3771 Aug 31 20:34 .bashrc
drwxrwxr-x 8 ubuntu ubuntu 4096 Aug 31 20:34 .git
-rw-rw-r-- 1 ubuntu ubuntu  807 Aug 31 20:34 .profile
-rw-rw-r-- 1 ubuntu ubuntu   59 Aug 31 20:34 main.py
```

 **Key Finding:** The `.git` directory confirms this is a Git repository. This hidden folder contains the **entire version history** — every commit, branch, and even deleted files.

---

### Step 2: Exploring Commit History

Now let's examine the commit timeline:

```bash
git log --all
```

**Output:**

```
commit c56c470a2a9dfb5cfbd54cd614a9fdb1644412b5 (HEAD -> master)
Author: developer <developer@example.com>
Date:   Sat Aug 31 15:30:00 2025 +0000

    Fixed the issue

commit 3a8cc16f919b8ac43651d68dceacbb28ebb9b625
Author: developer <developer@example.com>
Date:   Sat Aug 31 15:29:00 2025 +0000

    Initial commit
```

 **Analysis:** Two commits exist. The second one's message — "Fixed the issue" — is suspicious. What exactly was "fixed"? Let's investigate further.

---

### Step 3: Time Travel — Moving Between Commits

Let's jump to the second commit to see what the developer changed:

```bash
git checkout c56c470a2a9dfb5cfbd54cd614a9fdb1644412b5
```

Now, let's examine the contents of `main.py`:

```bash
cat main.py
```

 **Discovery:** Inside the file, we find a **hardcoded username**! This is a classic security vulnerability. Hardcoding credentials in source code means anyone with repository access can view them.

But wait — what if the previous commit contains even more sensitive data?

---

### Step 4: Going Deeper — The Initial Commit

Let's travel back to the very first commit:

```bash
git checkout 3a8cc16f919b8ac43651d68dceacbb28ebb9b625
```

Once again, we examine the file:

```bash
cat main.py
```

 **BINGO!** There it is — the flag, hidden in plain sight within the source code!

---

## The Flag

```
flag{a489-----------------------}
```

---

## 4. Why This Works — Deep Dive

### Git's Architecture

Git is designed as a **content-addressable filesystem**. When you commit changes:

1. Git creates a snapshot of all tracked files
2. This snapshot is stored as an object in the `.git/objects` directory
3. Even if you modify or delete files later, the original snapshots **remain forever**
4. Commits are linked in a chain, allowing full historical navigation

### The Danger of "Fixing" Sensitive Commits

When developers realize they've committed sensitive data, they often:

- Delete the sensitive lines
- Make a new commit with a message like "removed credentials" or "fixed issue"
- Push the changes and assume the problem is solved

**Why this fails:**

- The original commit still exists in the history
- Anyone with repository access can `git checkout` to any previous commit
- The sensitive data remains accessible unless the history is rewritten

---

## 5. Remediation — How to Actually Fix This

If you accidentally commit sensitive data, here are the proper steps:

### Option 1: Rewrite History (For Local/Private Repos)

```bash
git filter-branch --force --index-filter \\
"git rm --cached --ignore-unmatch PATH-TO-SENSITIVE-FILE" \\
--prune-empty --tag-name-filter cat -- --all
```

### Option 2: Use BFG Repo-Cleaner

```bash
bfg --delete-files SENSITIVE-FILE
```

### Option 3: Rotate Credentials Immediately

- If credentials were exposed, **change them immediately** — rewriting history doesn't invalidate leaked secrets
- Treat any exposed API keys, passwords, or tokens as compromised

---

## 6. Key Takeaways

| # | Lesson |
| --- | --- |
| 1 | **Git never forgets** — Once committed, data persists in history |
| 2 | **Commit messages matter** — Suspicious messages like "fixed" are red flags |
| 3 | **Never hardcode credentials** — Use environment variables or secret management |
| 4 | **History tells the story** — `git log`, `git show`, and `git diff` are forensic tools |
| 5 | **Forensics = Understanding WHY** — It's not just about finding flags, but understanding the underlying vulnerabilities |

---

## 7. Tools & Commands Used

| Command | Purpose |
| --- | --- |
| `ls -la` | List all files including hidden ones |
| `git log --all` | Display complete commit history |
| `git checkout <hash>` | Navigate to a specific commit snapshot |
| `cat main.py` | View file contents |

---

## 8. Conclusion

The Committed room teaches a fundamental lesson in **Git hygiene** and **secure development practices**. Source code repositories are forensic goldmines — every change, every mistake, and every "fix" is permanently recorded.

This challenge demonstrates why:

- Security awareness must extend to version control
- Code reviews should catch hardcoded secrets
- Proper secret management tools should always be used

---

## 9. References

- [TryHackMe - Committed Room](https://tryhackme.com/room/committed)
- [Git Official Documentation](https://git-scm.com/doc)
- [OWASP - Hardcoded Passwords](https://owasp.org/www-community/vulnerabilities/Use_of_hard_coded_password)

---

*Thanks for reading! If you found this write-up helpful, feel free to share and follow for more cybersecurity content.* 

---

**Tags:** #TryHackMe #CTF #Forensics #Git #CyberSecurity #WriteUp
