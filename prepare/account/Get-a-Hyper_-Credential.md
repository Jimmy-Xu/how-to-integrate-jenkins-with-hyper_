#Get a Hyper_ Credential
This part will show you how to get a Hyper_ Credential.

If you haven't an account on Hyper_ , then register a new user first. 
```
1. Sign Up on https://console.hyper.sh
2. A confirm email will be sent to your register email 
3. Login your email and click the confirm link to active your Hyper_ account.
```
![](/assets/hyper-console/1.register_hyper_user.PNG)

If you already have an Hyper_ account, then create a new credential.
```
1. Login https://console.hyper.sh
2. Goto https://console.hyper.sh/account/credential
3. Click the green "Create credential" button
4. Download your credential
```
![](/assets/hyper-console/2.account-setting.png)

![](/assets/hyper-console/3.create-credential.PNG)

That's all. You need provide this Hyper_ Credential when start jenkins container on Hyper_ like this:
```
$ hyper run -d --size=l --name jenkins-hyper-demo \
  -v jenkins-data:/var/jenkins_home \
  -e ACCESS_KEY=$ACCESS_KEY \
  -e SECRET_KEY=$SECRET_KEY \
  hyperhq/jenkins-hypercli:2.10
```

The image `hyperhq/jenkins-hypercli:2.10` is base on [jenkinsci/jenkins:2.10](https://hub.docker.com/r/jenkinsci/jenkins), there is a hyper cli installed in it.
This is the [Dockerfile](https://github.com/hyperhq/jenkins-hypercli-image/blob/jenkins-hypercli/Dockerfile#L65).