#Docker Image
## Jenkins server
* The image [`hyperhq/jenkins-hypercli:2.10`](https://hub.docker.com/r/hyperhq/jenkins-hypercli/) is base on [jenkinsci/jenkins:2.10](https://hub.docker.com/r/jenkinsci/jenkins). 
* There is a hyper cli installed in it(`use hyper cli to run temporary container to build project`).
* This is the [Dockerfile](https://github.com/hyperhq/jenkins-hypercli-image/blob/jenkins-hypercli/Dockerfile#L65).
## Build env for golang project
* This image [`hyperhq/jenkins-hyper-example-builder:latest`](https://hub.docker.com/r/hyperhq/jenkins-hyper-example-builder/) ) is base on [golang:1.5](https://hub.docker.com/_/golang/).
* There is a awscli installed in it(`use aws s3 cli to upload binary archive`).
* This is the [Dockerfile](https://github.com/hyperhq/jenkins-hyper-example-app/blob/master/Dockerfile#L17).
