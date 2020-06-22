# GitHub

## 0. GitHub Set-up
Configure Github commit name and email address
```
git config --global --edit
```

Generate SSH key
```
# check for ssh key, id_rsa.pub or similar should come back
ls -al ~/.ssh

# generate a new SSH key
ssh-keygen -t rsa -b 4096 -C "email@emailaddress"

# confirm file name, and enter passphrase
```

Add SSH key to ssh-agent so password doesn't need to be entered
```
# start the ssh agent
eval "$(ssh-agent -s)"
```
check the file `~/.ssh/config` contains
```
Host *
 AddKeysToAgent yes
 UseKeychain yes
 IdentityFile ~/.ssh/id_rsa
```
add your SSH private key to the AddKeysToAgent
```
ssh-add -K ~/.ssh/id_rsa
```

Add a new SSH key to Github account
```
# copy key to clipboard
pbcopy < ~/.ssh/id_rsa.pub
```
- go to [Github.com](https://github.com)
- top right, profile photo, go to Settings
- In the sidebar, click SSH and GPG keys
- create New SSH key, give it a title and paste in key

```
# Attempts to ssh to GitHub
ssh -T git@github.com
```

## 1. Create a Project directory and set-up with Github
Create a directory skeleton and README file and add to a new repo in Github.
```
mkdir {directory}
cd {directory}
touch README.md
touch .gitignore
```
Create a README.md file and add some text to it.

Create a repo in Github and commit a file.
```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/cg2p/{directory}.git
git push -u origin master
# or if really sure to force push
git push -u origin +master
```

## 2. Create a branch
Use a meaningful objective name e.g. `base-node-app`.
Only `master` is the deployable branch.

## 3. Add commits
Add, delete, update files is making commits to your branch.

```
// .git file in repo local copy tells details about remote
// check changes to happen
git status

// stage changes to happen, add commit message and push local to repo
git add .
git commit -m "update"
git push
```


