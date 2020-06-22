# Docker actions

## Docker Build and Repositories

Build multiple images
```
cd ~/echo-nextjs-client
docker build -t cg2p/echo-nextjs-client:0.0.1 .
docker push cg2p/echo-nextjs-client:0.0.1

cd ~/echo-service-with-mongo
docker build -t cg2p/echo-service-with-mongo:0.0.1 .
docker push cg2p/echo-service-with-mongo:0.0.1
```


## Docker on Local
Base build and run of app with Docker

### Clean up of local docker
```
# list images in repo
docker images ls

# list of image id
docker images -q

# remove all images
docker rmi `docker images -q`
```

### Local Build and Run Example
```
cd reverse-with-nextjs-material
docker build -t reverse-app:1.0 .
docker image ls

# - p <host port>:<container port>
# <container port> is the one the app listens on 
docker run -p 3002:3000 --detach --name reverse-app reverse-app:1.0
```
Test http://localhost:3002

Stop the container
```
docker container ls
docker container stop <container id>
```

Create a docker compose yml
```
version: '2.0'
services:
  web:
    build: .
    ports:
    - "3003:3000"
```
then run with docker compose
```
docker-compose up & // test on http://localhost:3003
docker-compose down
```