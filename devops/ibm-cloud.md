# IBM Cloud

[IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-getting-started)

## installation
Installation or update this set of tools:

- Homebrew (Mac only)
- Git
- Docker
- Helm
- kubectl
- IBM Cloud Functions plug-in
- IBM Cloud Object Storage plug-in
- IBM Cloud Container Registry plug-in
- IBM Cloud Kubernetes Service plug-in

```
curl -sL https://ibm.biz/idt-installer | bash
// restart the shell to use `ic`
ic dev help
```

curl -u XxB8GYIz8_FiDq6OgDq05oRnYS-IIzksmUYO9KQs-7T7 POST https://eu-gb.functions.cloud.ibm.com/api/v1/namespaces/screenwritersplatform%40gmail.com_dev/actions/hello-world/helloworld?blocking=true

curl -d '{ "name" : "smith" }' -u 3aee0f87-8f99-41ff-ae93-ccb214656061:jSJpikkAkUF3DskrIRLVIkBXfVkgwf2zU50rBv8S7s3UMLOBUWvMUJgz7IQpXRA1 POST https://eu-gb.functions.cloud.ibm.com/api/v1/namespaces/screenwritersplatform%40gmail.com_dev/actions/hello-world/helloworld?blocking=true


## free IKS cluster
after cluster provision
```
ibmcloud login -a cloud.ibm.com -r us-south -g swp-dev
ibmcloud ks cluster config --cluster bqlqn48d0lg57mo9uh0g
kubectl config current-context
```

## Container registry

```
# pick the right region
ibmcloud cr region-set

# clean up
ibmcloud cr namespace-list
> Listing namespaces for account 'Jeremy Caine's Account' in registry 'jp.icr.io'...
> cg2p

ibmcloud cr retention-run --images 1 cg2p
```

## coligo
```
ibmcloud plugin install coligo

```