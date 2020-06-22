# Development environment

## 1. Setup Mac

### Bash profile
add to `vi .bash_profile`

```
alias la='ls -al’`
```

### Enable root
https://support.apple.com/en-gb/HT204012

```
su root
```

### Install XCode
Xcode from app store

### Install Brew
https://brew.sh/

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Then checks and update
```
brew update // check latest
brew doctor // update latest
brew prune // cleans up broken symlinks
brew cask // missing app manager for Mac
```

## 2. Code

### Atom
https://atom.io/

### Node
Install node.js and npm
choose macOS installer
https://nodejs.org/en/download/

check PATH has /usr/local/bin

```
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```
### Git
Install git
https://git-scm.com/downloads
or via brew
```
brew install git // uplifts from git via Apple XCode
brew info git
```
### Go language
https://golang.org/dl/


### Docker
https://store.docker.com/editions/community/docker-ce-desktop-mac

