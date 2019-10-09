# Node.js Cloud Native Study Project
Using
- node.js
- docker
## Reference
- Cloud Native Development with Node.js, Docker, and Kubernetes by LinkedIn
  - https://www.linkedin.com/learning/cloud-native-development-with-node-js-docker-and-kubernetes/creating-your-node-js-app


## Create a node.js application
```
  npm install experss-generator -g

  express myapp

  cd myapp

  npm install

  npm start
```

## Create docker image
download docker image template from  https://www.cloudnativejs.io/
then https://github.com/CloudNativeJS/docker

.dockerignore determains the files are not been copied to docker image.

```
wget https://raw.githubusercontent.com/CloudNativeJS/docker/master/Dockerfile
wget https://raw.githubusercontent.com/CloudNativeJS/docker/master/.dockerignore

# build docker image at current directory and copy source code into it
# -t is the tag of the docker image
docker build -t nodeserver  -f Dockerfile .  

docker images

docker run -i -p 3721:3721 -t nodeserver
```

## Create dev and debug environment for Docker
```
wget https://raw.githubusercontent.com/CloudNativeJS/docker/master/Dockerfile-tools
wget https://raw.githubusercontent.com/CloudNativeJS/docker/master/run-dev
wget https://raw.githubusercontent.com/CloudNativeJS/docker/master/run-debug
```
Modify those files to work with the code created by express-generator

build docker image for debugging
```
  docker build -t myserver-tools  -f Dockerfile-tools . 
```
Generate a Linux version of your node_modules dependencies locally, by generating them inside the node:10 docker image
Copy package.json into image and run npm install
```
  docker run -i -v "$PWD"/package.json:/tmp/package.json -v "$PWD"/node_modules_linux:/tmp/node_modules -w /tmp -t node:10 npm install
```
Run app in develop docker
```
  docker run -i -p 3000:3000 -p 9229:9229 -t myserver-tools /bin/run-debug
```
Using chrom connect to the server
```
  chrom://inspect
```
## Create run version Docker image

```
wget https://raw.githubusercontent.com/CloudNativeJS/docker/master/Dockerfile-run
```
The running Docker image is based on node:10-slim for Node.js app
```
  docker build -t nodeserver-run -f Dockerfile-run
  docker run -i -p 3000:3000 -p 9229:9229 -t nodeserver-run
```

## Tag and version control
```
  docker tag nodeserver-run nodeserver:1.0.0
```
Publish
```
  docker login
  docker push username/name-of-image:tag
```

