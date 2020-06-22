#  Minishift

## Set-up
https://docs.okd.io/latest/minishift/index.html

https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#for-macos 


## Clean Up
```
minishift delete
brew uninstall docker-machine-driver-xhyve
brew uninstall docker-machine-driver-hyperkit
rm -rf (E.g /usr/local/bin/docker-machine-driver-xhyve)
rm -rf config files .docker .kube .minishift .minikube
```

## Docker
install Docker Desktop for Mac
change to github.com code directory
```
cd doodle/cheers2019
docker build -t cg2p/cheers2019 .
docker run -it --rm cg2p/cheers2019
```

## Setting Up the Virtualization Environment - Hyperkit
```
brew install hyperkit
brew link --overwrite hyperkit
brew install docker-machine-driver-hyperkit
sudo chown root:wheel /usr/local/opt/docker-machine-driver-hyperkit/bin/docker-machine-driver-hyperkit
sudo chmod u+s /usr/local/opt/docker-machine-driver-hyperkit/bin/docker-machine-driver-hyperkit
brew info docker-machine-driver-hyperkit

brew install docker-machine-driver-xhyve
sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
```

## Install minishift
via Homebrew
```
brew cask install --force minishift
```

curl -LO https://storage.googleapis.com/minikube/releases/latest/docker-machine-driver-hyperkit && sudo install -o root -g wheel -m 4755 docker-machine-driver-hyperkit /usr/local/bin/


## Minishift Quickstart
if minishift start fails
- go to github, Settings, developer settings, personal access tokes
- regenerate minishift token
You might have regenerate github minishift token
`export MINISHIFT_GITHUB_API_TOKEN=<token-id>`

```
minishift stop
minishift delete
cd
rm -rf ~/.minishift
minishift config set vm-driver hyperkit
minishift start -v 10
```
go to browser link
    User:     developer
    Password: developer

```
minishift oc-env
```
add to PATH in profile and eval
test `oc`
```
oc new-app https://github.com/sclorg/nodejs-ex -l name=myapp
oc logs -f bc/nodejs-ex
oc expose svc/nodejs-ex
minishift openshift service nodejs-ex --in-browser

```
create an app from my repo
```
minishift start 
oc new-app https://github.com/cg2p/echo-nextjs

```