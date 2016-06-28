#Get an AWS S3 Credential
This part will show you how to get an AWS S3 Credential.

First you need an AWS account, login and goto https://console.aws.amazon.com/iam/home#users
```
1. Click blue "Create New Users" button, Enter User Names, for example "hyper_s3_demo"
2. Click blue "Download Credentials" button to save the AWS S3 Credentials
3. Click the new user, Click blue "Attach Policy" button under "Permissions" Tab, add the policy "AmazonS3FullAccess"
```

![](/assets/aws-console/1.download-aws-credential.png)

![](/assets/aws-console/2.attach-policy.PNG)


Then, you can create a new S3 bucket on https://console.aws.amazon.com/s3
```
1. Click blue "Create Bucket" button
2. Input the "Bucket Name", for example "jenkins-hyper-example-app"
3. Select a Region, for example "Northern California"
```
![](/assets/aws-console/3.create-s3-bucket.png)


That's all. You need provide this AWS S3 Credential and S3 Bucket when start Hyper_ container in Jenkins's Command of "Execute shell" like this:

```
### start new container
AWS_ACCESS_KEY=AKIxxxxxxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_S3_BUCKET=jenkins-hyper-example-app
hyper run -d --name jenkins-hyper-example-builder \
 --size=l \
 -e AWS_ACCESS_KEY=$AWS_ACCESS_KEY \
 -e AWS_SECRET_KEY=$AWS_SECRET_KEY \
 -e AWS_S3_BUCKET=$AWS_S3_BUCKET \
 hyperhq/jenkins-hyper-example-builder
```