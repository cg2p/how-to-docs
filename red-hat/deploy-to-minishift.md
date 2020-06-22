# Kubernetes on Minishift
Goal is to build and deploy and app onto Kubernetes cluster running on Minishift

Using a simple NextJS (React SSR) app [reverse-app](https://github.com/cg2p/reverse-with-nextjs-material)

1. build and run reverse-app with Docker
2. deploy docker image to minishift k8s using commands
3. deploy docker image to minishift k8s with config yaml

## Manually Deploy to Minishift
Deploy docker image to minishift k8s using commands

```
eval $(minishift oc-env)
oc status // returns current project
# create new project
oc new-project reverse-project --description="for the reverse app" --display-name="Reverse Project"
oc status
```

```
# build from remote git repo
oc new-app https://github.com/cg2p/reverse-with-nextjs-material
# track build
oc logs -f bc/reverse-with-nextjs-material
oc expose svc/reverse-with-nextjs-material

# test on http://reverse-with-nextjs-material-reverse-project.192.168.64.4.nip.io

```

##  Tekton on Minishift
https://github.com/tektoncd/pipeline/blob/master/docs/install.md#installing-tekton-pipelines-on-openshift 

```
oc logout
oc login -u system:admin
oc new-project tekton-pipelines
oc adm policy add-scc-to-user anyuid -z tekton-pipelines-controller
oc apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.notags.yaml
oc get pods --namespace tekton-pipelines --watch // ctrl+c to stop
```

## Minikube
1. create a k8s cluster
2. deploy an app
3. explore the app
4. expose the app publicly
5. scale up the app
6. update the app



