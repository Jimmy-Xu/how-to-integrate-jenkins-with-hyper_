# Get a GitHub Token
This part will show you how to get a github personal access token.

First you need a github account, login and goto https://github.com/settings/tokens
```
1. Click the grey "generate new token" button
2. Input the "Token description", for example "jenkins-hyper-demo"
3. "Select scopes" of this token, check all checkbox for "repo" and "admin:repo_hook"
4. Click the green "Generate token" button.
5. Copy and save the new token(the value of this token will occur just once)
```
![](/assets/jenkins-github/1.create-personal-token.PNG)

That's all. This token will be used in Jenkins(http://23.236.114.227:8080/configure) like this: 
```
Manage Jenkins -> Configure System ->  GitHub Servers
  -> Add GitHub Server
     API URL: "https://api.github.com"
     Credentials: 
        Kind: "Secret text"
        Secret: <github personal access token>
        ID: [example: jenkins-hyper-demo]
        Description: [example: github token]
```
![](/assets/jenkins-github/3.use-personal-token-in-jenkins.png)

Jenkins will create github webhook by this personal access token.