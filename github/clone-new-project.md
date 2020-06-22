# Clone an existing project into a new one

```
mkdir [folder name]
git clone https://github.com/xxx/[repo].git [folder name]
cd [folder name]
git init // to point to new repo
git remote rm origin
```

Now go to `github` and create a new repo , then

```
git add .
git remote add origin https://github.com/cg2p/[new repo].git
git push -u origin master
```