# Code Ready Containers
Procedure for installing CRC - aka Openshift 4.x - onto local laptop. 

Using macOS Catalina 10.15.5. 

## Installation
https://access.redhat.com/documentation/en-us/red_hat_codeready_containers/1.0/html/getting_started_guide/getting-started-with-codeready-containers_gsg

- download CRC, extract and move to folder in your PATH
- in Mac Finder, right click Open on `crc`
- go through verifying developer process, accept with Open
- go and get your pull secret from Red Hat
- https://cloud.redhat.com/openshift/install/crc/installer-provisioned 
- Copy Pull Secret or download
- now you can move to the `crc setup` instructions

## Set-up
```
crc setup
crc start
```
Startup asks for pull secret (one-time), paste in and CRC will finish install

## Usages
1. Start CRC and log into web console
```
crc start
crc console
```
You will need to accept browser security risk, to serve locally.
Then web console login options as `kube:admin` or `htpasswd_provider` (u developer, p developer)

2. To access CRC OpenShift cluster using `oc`
```
crc oc-env
```
It returns the commands to add ot profile so you can work with oc against CRC

> export PATH="/Users/jeremycaine/.crc/bin/oc:$PATH"
> # Run this command to configure your shell:
> # eval $(crc oc-env)

3. Login and interact with cluster using `oc`. Access as developer or admin.
These commands (specific to your install) were shown when `crc start` was executed.
```
oc login -u developer -p developer https://api.crc.testing:6443
oc login -u kubeadmin -p 8rynV-SeYLc-h8Ij7-YPYcz https://api.crc.testing:6443
```

As developer you can start by creating a project.
As admin, you can check the cluster for info e.g. `oc get co`
CRC OpenShift now up and running.

4. Shutdown
Stop the OpenShift cluster
```
crc stop
```

Delete the Code Ready container virtual machine and lose all changes to OpenShift cluster.
```
crc delete
```