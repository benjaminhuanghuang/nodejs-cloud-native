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


