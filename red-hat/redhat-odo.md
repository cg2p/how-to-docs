# Red Hat odo

https://docs.openshift.com/container-platform/4.3/cli_reference/openshift_developer_cli/understanding-odo.html 

## install
odo
```
curl -L https://mirror.openshift.com/pub/openshift-v4/clients/odo/latest/odo-darwin-amd64 -o /usr/local/bin/odo
chmod +x /usr/local/bin/odo
```

maven
```
brew install maven
```

test odo and minishift
```
export MINISHIFT_GITHUB_API_TOKEN=<tokenid>
minishift start
odo login -u developer -p developer
odo catalog list components
```

## Creating a multicomponent application with odo

```
odo project create echo-app
mkdir echo-app && cd echo-app
mkdir echo-service-with-mongo && cd echo-service-with-mongo
odo create nodejs backend --git https://github.com/cg2p/echo-service-with-mongo.git
odo push
cd ..
mkdir echo-nextjs-client && cd echo-nextjs-client
odo create nodejs frontend --git https://github.com/cg2p/echo-nextjs-client.git
odo push
odo list
odo link backend --port 8080
```
which outputs
    ✓  Component backend has been successfully linked to the component frontend

    The below secret environment variables were added to the 'frontend' component:

    · COMPONENT_BACKEND_PORT
    · COMPONENT_BACKEND_HOST

    You can now access the environment variables from within the component pod, for example:
    $COMPONENT_BACKEND_HOST is now available as a variable within component frontend

```
odo url create frontend --port 8080
odo push
```
which outputs
    Validation
    ✓  Checking component [15ms]

    Configuration changes
    ✓  Retrieving component data [25ms]
    ✓  Triggering build from git [35ms]
    ✓  Waiting for build to finish [50s]
    ✓  Applying configuration [12s]

    Applying URL changes
    ✓  URL frontend: http://frontend-app-swp-app.192.168.64.3.nip.io created

    Pushing to component frontend of type git
    ✓  Changes successfully pushed to component

 ```
 > http://frontend-app-swp-app.192.168.64.3.nip.io

 ```