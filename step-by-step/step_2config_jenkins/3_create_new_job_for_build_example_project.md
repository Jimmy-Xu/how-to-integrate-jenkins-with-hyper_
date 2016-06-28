# 3) create new job for build example project


- Require:  
  - AWS S3 credential
  - S3 Bucket

##create New Item in Jenkins
![](/assets/jenkins-job/1.new-job.png)

## Set Item Name and Type
![](/assets/jenkins-job/2.set-job-name-and-type.png)

## Set Source Code Management

Set https://github.com/hyperhq/jenkins-hyper-example-app as `Repository URL`

![](/assets/jenkins-job/3.set-source-management.png)

## Add Credentials for github

> It's used for clone project to jenkins workspace.  
> It's optional for public github repo

![](/assets/jenkins-job/4.add-github-token-in-jenkins.png)

## Set Build Trigger

> Jenkins build job will start automatically when receive the github push event

![](/assets/jenkins-job/5.build-when-github-push.PNG)

## A GitHub webhook will be created by Jenkins
![](/assets/jenkins-job/6.auto-create-github-webhook.PNG)

## Add "Execute Shell" as a Build Step (`The most important part`)

![](/assets/jenkins-job/7.build-execute-shell.png)


>The following is the content of Command:

```bash
### prepare
# remove old container
(hyper ps -a | grep jenkins-hyper-example-builder) && hyper rm -f jenkins-hyper-example-builder
# pull new image
hyper pull hyperhq/jenkins-hyper-example-builder

### start new container (set AWS S3 Credential and S3 Bucket here)
AWS_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_S3_BUCKET=jenkins-hyper-example-app
hyper run -d --name jenkins-hyper-example-builder \
 --size=l \
 -e AWS_ACCESS_KEY=$AWS_ACCESS_KEY \
 -e AWS_SECRET_KEY=$AWS_SECRET_KEY \
 -e AWS_S3_BUCKET=$AWS_S3_BUCKET \
 hyperhq/jenkins-hyper-example-builder

### start deploy in container ( unit-test -> make -> integration-test -> upload )
# clone source from github
hyper exec -i jenkins-hyper-example-builder /step.sh clone
# start deploy
hyper exec -i jenkins-hyper-example-builder /go/src/github.com/hyperhq/jenkins-hyper-example-app/auto.sh

### clear container
hyper stop jenkins-hyper-example-builder
hyper rm jenkins-hyper-example-builder

```
