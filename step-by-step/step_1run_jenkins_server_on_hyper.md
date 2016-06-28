
## Step 1. Run jenkins server on Hyper_

- Require:  
  - Hyper_ credential
  - [hyper cli](https://docs.hyper.sh/GettingStarted/install.html)
  - image on docker hub: [hyperhq/jenkins-hypercli:2.10](https://hub.docker.com/r/hyperhq/jenkins-hypercli/)

Run the following command in your local HostOS:
```bash
// allocate public ip
$ hyper fip allocate 1
23.236.114.227

// create volume
$ hyper volume create --name jenkins-data

// run jenkins container(use Hyper_ Credential here)
$ ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxx
$ SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxx
$ hyper run -d --name jenkins-hyper-demo \
    --size=l \
    -v jenkins-data:/var/jenkins_home \
    -e ACCESS_KEY=$ACCESS_KEY \
    -e SECRET_KEY=$SECRET_KEY \
    hyperhq/jenkins-hypercli:2.10

// associate public ip to jenkins container
$ hyper fip associate 23.236.114.227 jenkins-hyper-demo

// test hypercli in jenkins container(show tenantid of Hyper_)
$ hyper exec -it jenkins-hyper-demo hyper info | grep ID
ID: 56bfa4e8063c4872axxxxxxxxxxxxxxx

// get Jenkins unlock password
$ hyper logs jenkins-hyper-demo
...
*************************************************************
*************************************************************
*************************************************************
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

e85299cb69274de48f5a09xxxxxxxxxxxxxx
...

$ hyper ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED        STATUS        PORTS                        NAMES               PUBLIC IP
60aaf8d60c4d   hyperhq/jenkins-hypercli:2.10   "/bin/tini -- /usr/lo"   11 hours ago   Up 11 hours   0.0.0.0:8080->8080/tcp,...   jenkins-hyper-demo  23.236.114.227
```

Of course, the Jenkins server don't have to be hosted on Hyper_.  
The key is to `install Jenkins and hyper cli together`.  
For example, you can run the Jenkins server with docker on your own host.
Here is an example run jenkins server with docker  
```
$ mkdir -p $(pwd)/jenkins-data
$ ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxx
$ SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxx
$ docker run -d --name jenkins-hyper-demo \
  -v $(pwd)/jenkins-data:/var/jenkins_home \
  -p 8080:8080 \
  -p 50000:50000 \
  -e ACCESS_KEY=$ACCESS_KEY \
  -e SECRET_KEY=$SECRET_KEY \
  hyperhq/jenkins-hypercli:2.10
//get tenantid to test the connection to Hyper_
$ docker exec -it jenkins-hyper-demo hyper info | grep ID
```
But if you want to receive GitHub webhook to trigger Jenkins to start build, you need a public ip for this container.  
