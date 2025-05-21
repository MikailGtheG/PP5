# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
# and the relevant terminal output (e.g., branch listing, merge messages)
```
## Task 1: Local Git – Branching & Merging

### Steps I followed

```bash
# Step 1: Clone the repository from GitHub
git clone https://github.com/MikailGtheG/PP5

# Step 2: Create a new directory and initialize it as a Git repo (not strictly needed, just to show init)
mkdir PP5_1
cd PP5_1
git init
cd ..

# Step 3: Go into the cloned project
cd PP5

# Step 4: Create a new branch called feature-1
git checkout -b feature-1

# Step 5: Create a new file with some content
echo "Dies ist der feature-1 Branch, in dem ich neue Features teste." > hello.txt

# Step 6: Add the file to staging area
git add hello.txt

# Step 7: Commit the changes
git commit -m "Add hello.txt with feature-1 description"

# Step 8: Go back to master branch
git checkout master

# Step 9: Merge feature-1 into master
git merge feature-1
```
### Terminal-Output:

```bash
Cloning into 'PP5'...
remote: Enumerating objects: 10, done.
...
Branch 'feature-1' set up to track remote branch 'feature-1' from 'origin'.

[feature-1 cf257f6] Add hello.txt with feature-1 description
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt

Switched to branch 'master'
Your branch is up to date with 'origin/master'.

Updating bd8e694..cf257f6
Fast-forward
 hello.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
```
---

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs
```

### SSH into the Server and Create Bare Repository

```bash
ssh user58@128.140.85.215
```

Enter your password when prompted.

```bash
mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare
```

Output:
```
Initialized empty Git repository in /home/user58/repos/myproject.git/
```

Then exit the server:
```bash
exit
```

---

### Add Remote Repository on Local Machine

```bash
git remote remove origin-ssh
git remote add origin-ssh user58@128.140.85.215:~/repos/myproject.git
git remote -v
```

Output:
```
origin       https://github.com/MikailGtheG/PP5 (fetch)
origin       https://github.com/MikailGtheG/PP5 (push)
origin-ssh   user58@128.140.85.215:~/repos/myproject.git (fetch)
origin-ssh   user58@128.140.85.215:~/repos/myproject.git (push)
```

---

### Push Local Repository to Remote

```bash
git push origin-ssh master
```

Output:
```
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 5.32 KiB | 5.32 MiB/s, done.
Total 13 (delta 2), reused 9 (delta 1), pack-reused 0
To 128.140.85.215:~/repos/myproject.git
 * [new branch]      master -> master
```

---

### Clone the Repository into a Fresh Directory

```bash
cd ~/Schreibtisch
git clone user58@128.140.85.215:~/repos/myproject.git
```

Output:
```
Cloning into 'myproject'...
remote: Enumerating objects: 13, done.
remote: Counting objects: 100% (13/13), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 13 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (13/13), 5.32 KiB | 5.32 MiB/s, done.
Resolving deltas: 100% (2/2), done.
```

---

### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs
```

---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
* GitLab MR: *paste URL and a one-sentence summary*

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
