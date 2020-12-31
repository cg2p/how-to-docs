# End to End Build and Deploy to OpenShift

## Create ROKS cluster on IBM Cloud
IBM account
cluster: `caine-roks-dal`
OCP version 4.4

## Installs
[oc CLI on laptop](https://docs.openshift.com/container-platform/4.4/cli_reference/openshift_cli/getting-started-cli.html)

## Accessing cluster on IBM Cloud
[Access ROKS cluster on IBM Cloud](https://cloud.ibm.com/docs/openshift?topic=openshift-access_cluster)

1. via OpenShift oauth token request page
```
oc login --token=BsXRerXnUvqI9pYofGZrl8v8SqJfbTG1IAz3AmzRFNE --server=https://c106-e.us-south.containers.cloud.ibm.com:30545
```

2. via CLI
```
# log into IBM Cloud
ibmcloud login --sso
# get OTP passcode
# select account

# get Master URL
ibmcloud oc cluster get -c caine-roks-dal
> Master URL: https://c106-e.us-south.containers.cloud.ibm.com:30545

oc login -u passcode --server=https://c106-e.us-south.containers.cloud.ibm.com:30545
oc login -u passcode -p fDxxqhZJPx --server=https://c106-e.us-south.containers.cloud.ibm.com:30545
2OrIx6KInG
y
# login is successful, set to default project
oc projects
```

## Project and App
```
oc new-project reverse
oc new-app https://github.com/cg2p/openshift-reverse
oc status
```

```
# expose the port that the Kubernetes deployment is set to expose container on
oc expose dc/openshift-reverse --port=3000
oc expose service/openshift-reverse

oc get route
> get HOST/PORT url and test app
```

## OpenShift Pipelines
[Install Pipeline to Cluster](https://github.com/openshift/pipelines-tutorial/blob/master/install-operator.md)

OpenShift WebConsole > Admin > Operator > OperatorHub > find 'OpenShift Pipelines Operator'
Install and Creset Update Channel to 'ocp-4.4'

[Install Pipeline CLI](https://docs.openshift.com/container-platform/4.4/cli_reference/tkn_cli/installing-tkn.html#installing-tkn)

[Pipelines tutorial](https://github.com/openshift/pipelines-tutorial)
```
oc get serviceaccount pipeline
```

Get reusable Tasks for Pipelines
```
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-1/01_pipeline/01_apply_manifest_task.yaml
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/release-tech-preview-1/01_pipeline/02_update_deployment_task.yaml
tkn task list
tkn clustertasks list
```

Create the pipeline
```
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/04_pipeline.yaml
tkn pipeline ls
```

Pipeline run
```
tkn pipeline start build-and-deploy \
    -w name=shared-workspace,volumeClaimTemplateFile=https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/03_persistent_volume_claim.yaml \
    -p deployment-name=reverse-app \
    -p git-url=https://github.com/cg2p/openshift-reverse.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000

tkn pipeline start build-and-deploy \
    -w name=shared-workspace,volumeClaimTemplateFile=https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/03_persistent_volume_claim.yaml \
    -p deployment-name=reverse-app \
    -p git-url=https://github.com/cg2p/openshift-reverse.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000/reverse/reverse-app \
```

```
oc new-project pipelines-tutorial
oc get serviceaccount pipeline
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/01_apply_manifest_task.yaml
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/02_update_deployment_task.yaml
tkn task ls
tkn clustertask ls
oc create -f https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/04_pipeline.yaml
tkn pipeline ls

tkn pipeline start build-and-deploy \
    -w name=shared-workspace,volumeClaimTemplateFile=https://raw.githubusercontent.com/openshift/pipelines-tutorial/master/01_pipeline/03_persistent_volume_claim.yaml \
    -p deployment-name=vote-api \
    -p git-url=http://github.com/openshift-pipelines/vote-api.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000/pipelines-tutorial/vote-api \



