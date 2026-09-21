# Lab 2 Notes

## Objective
Practice using Git and GitHub to manage a project, track changes, and keep work organized.
## Commands used
```bash
ls -l
chmod
pwd
cd
mkdir
touch
cat
grep
ssh-keygen -t ed25519
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
ssh -T git@github.com
git clone git@github.com:Blin-35/Lab-Practice.git
git switch -c lab-1-notes
git add
git commit
git push
git pull
git status
## What happened
I created a GitHub repository and connected to it from my Mac using SSH. I cloned the repository, created notes files, staged changes, committed them, and pushed them to GitHub.
I created branches for separate pieces of work, opened pull requests, reviewed the changes, and merged them into the main branch. I also created a .gitignore file to keep private keys, environment files, and system files from being uploaded.
## What I learned
A repository is an organized project space that stores files and their history. A branch lets me work on a change separately from the main project. A commit is a saved checkpoint, and a push uploads local commits to GitHub. A pull downloads changes from GitHub to my Mac.
SSH allows my Mac to authenticate with GitHub securely without using my GitHub password. Public keys can be shared with GitHub, but private keys must remain secret.
Pull requests let me review changes before merging them into the main branch. Public repositories can be viewed by anyone, while private repositories are better for school work or sensitive material.