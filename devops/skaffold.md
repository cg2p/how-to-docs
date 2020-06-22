# Skaffold
Skaffold handles the workflow for building, pushing and deploying an application. Open source project from Google.

## Install
macOS
```
brew install skaffold
```
> start Docker
> 

## First run against Minikube
Start minikube (which runs the Docker daemon that skaffold uses)
```
minikube start
eval $(minikube docker-env)
```

create a skaffold yaml config file
```
cd [project source dir]
skaffold init
```

different options to build and run
```
# build and run in watch mode
skaffold dev
```

## Configure to run against CRC (OpenShift 4.x)
> start Docker
```
brew cask install podman
crc start
eval $(crc oc-env)

oc login -u kubeadmin -p 8rynV-SeYLc-h8Ij7-YPYcz https://api.crc.testing:6443

oc patch configs.imageregistry.operator.openshift.io/cluster --patch '{"spec":{"defaultRoute":true}}' --type=merge

HOST=$(oc get route default-route -n openshift-image-registry --template='{{ .spec.host }}')
oc whoami -t
podman login --username $(oc whoami) --tls-verify=false $HOST 
podman login --username $(oc whoami) $HOST 

oc whoami -t | docker login -u kubeadmin  https://default-route-openshift-image-registry.apps-crc.testing

oc login -u kubeadmin -p <blah> https://api.crc.testing:6443 
oc whoami -t | docker login -u kubeadmin --password-stdin  https://default-route-openshift-image-registry.apps-crc.testing


# https://github.com/openshift/origin/issues/21691
# https://access.redhat.com/documentation/en-us/openshift_container_platform/4.2/html/cli_tools/openshift-cli-oc#cli-using-cli_cli-developer-commands
# https://github.com/openshift/origin/issues/21691
# https://github.com/openshift/image-registry/issues/205

# expose the registry so that skaffold can build crc images
# https://docs.openshift.com/container-platform/4.2/registry/securing-exposing-registry.html

other refs
https://hasura.io/blog/draft-vs-gitkube-vs-helm-vs-ksonnet-vs-metaparticle-vs-skaffold-f5aa9561f948/
 