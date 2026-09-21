# Lab 2 Notes

## Objective
HEAD

Practice using Git and GitHub to manage a project, track changes, and keep work organized.

Practice using Git and GitHub to manage a project, track changes, and keep work organized. The goal was to learn how to create and use a repository, connect securely, create branches, stage and commit work, and collaborate using pull requests.
 10fa0f4 (Update Lab 2 notes with objective, commands, errors, solutions, and lessons learned)

## Commands used

```bash
ls -l
pwd
cd
mkdir
touch
cat
grep
chmod
ssh-keygen -t ed25519
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
ssh -T git@github.com
git clone git@github.com:Blin-35/Lab-Practice.git
git switch -c lab-1-notes
git status
 HEAD
```

## What happened

I created a GitHub repository and connected to it from my Mac using SSH. I cloned the repository, created notes files, staged changes, committed them, and pushed them to GitHub.

I created branches for separate pieces of work, opened pull requests, reviewed the changes, and merged them into the main branch. I also created a `.gitignore` file to keep private keys, environment files, and system files from being uploaded.

## What I learned

A repository is an organized project space that stores files and their history. A branch lets me work on a change separately from the main project. A commit is a saved checkpoint, and a push uploads local commits to GitHub. A pull downloads changes from GitHub to my Mac.

SSH allows my Mac to authenticate with GitHub securely without using my GitHub password. Public keys can be shared with GitHub, but private keys must remain secret.

Pull requests let me review changes before merging them into the main branch. Public repositories can be viewed by anyone, while private repositories are better for school work or sensitive material.

git add .
git commit -m "Add lab notes"
git push origin lab-1-notes
git pull
```

### What these commands were used for
- `ls -l`: showed the files and folders in the current directory.
- `pwd`: confirmed the current working location.
- `cd`: moved between folders.
- `mkdir`: created a new directory.
- `touch`: created new files.
- `cat`: displayed file content.
- `grep`: searched files for text.
- `chmod`: changed file permissions when needed.
- `ssh-keygen -t ed25519`: created an SSH key for secure GitHub access.
- `ssh-add --apple-use-keychain ~/.ssh/id_ed25519`: added the private key to the macOS keychain.
- `ssh -T git@github.com`: tested whether GitHub recognized the SSH connection.
- `git clone ...`: copied the repository to my local machine.
- `git switch -c ...`: created a new working branch.
- `git status`: checked which files changed and what was staged.
- `git add .`: staged the changes for commit.
- `git commit -m ...`: saved the changes with a message.
- `git push origin ...`: uploaded the branch to GitHub.
- `git pull`: updated the local branch with the newest remote changes.

## Errors encountered
### 1. SSH authentication problems
When I tried to connect to GitHub with SSH, the terminal reported that authentication failed or the key was not accepted.

### 2. Untracked or modified files during work
Some files were not yet staged, so Git showed them as untracked or modified before I was ready to commit.

## Solutions
### SSH authentication fix
I generated a new SSH key using `ssh-keygen -t ed25519`, then added it to the keychain with `ssh-add --apple-use-keychain ~/.ssh/id_ed25519`. After confirming the public key was added to GitHub, I tested the connection with `ssh -T git@github.com` and completed the repo setup.

### File tracking fix
I used `git status` to check what was changed, then used `git add .` to stage the updated files. After that, I created a commit with `git commit -m "Add lab notes"` and pushed the branch with `git push origin lab-1-notes`.

## Lessons learned
- Git keeps a record of file history, which makes it easier to track and revise work.
- Branches help keep separate tasks organized without affecting the main project.
- SSH is a safer way to authenticate with GitHub than using a password every time.
- `git status` is a useful command for checking the state of the repository before committing.
- Pull requests make it easier to review and approve changes before merging them.
- It is important to check file permissions, key setup, and repository status before troubleshooting larger issues.

## Security note
This lab documentation does not include passwords, private keys, or any restricted school information.
 10fa0f4 (Update Lab 2 notes with objective, commands, errors, solutions, and lessons learned)
