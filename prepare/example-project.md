
#Example Project

>jenkins-hyper-example-app

* Description: 
  * this is a golang example project, output a binary file "reverse"
    * usage： `./reverse hello world`, output `dlrow olleh`
  * this project will be build(`pull code-> unit-test-> make-> integration-test-> upload`) in a container with a golang env
  * there is a pre-build image( [hyperhq/jenkins-hyper-example-builder](https://hub.docker.com/r/hyperhq/jenkins-hyper-example-builder/) ) for build this project
* Source Code(public repo): https://github.com/hyperhq/jenkins-hyper-example-app
