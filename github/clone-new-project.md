# Clone an existing project into a new one

Go to `github` and create a new repo [new repo]
```
git clone https://github.com/xxx/[repo].git [folder name]
cd [folder name]
git init // to point to new repo
git remote rm origin
git add .
git remote add origin https://github.com/cg2p/[new repo]
git push -u origin master
```
