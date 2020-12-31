# OpenShift Pipelines (Tekton)
[openshift-pipelines-tutorial](https://redhat-developer-demos.github.io/openshift-pipelines-workshop/)

## Pre-reqs for Local

1. CRC installed
2. Install tekton command line `tk`
```
brew tap tektoncd/tools
brew install tektoncd/tools/tektoncd-cli
ln -s /usr/local/bin/tkn /usr/local/bin/kubectl-tkn // create tekton as kubectl plugin
kubectl plugin list
>> /usr/local/bin/kubectl-tkn
```

