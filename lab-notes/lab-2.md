# Lab 2 Notes

## Objective

Practice using Git and GitHub to manage a project, track changes, and keep work organized. The goal was to learn how to create and use a repository, connect securely, create branches, stage and commit work, and collaborate using pull requests.

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
git add .
git commit -m "Add lab notes"
git push origin lab-1-notes
git pull