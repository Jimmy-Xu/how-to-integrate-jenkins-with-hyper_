# 2) add github server

# Generate new personal access token in GitHub

**goto https://github.com/settings/tokens**

> this token will be used in Jenkins to create github webhook, then Jenkins can receive trigger event from github.

![](/assets/jenkins-github/1.create-personal-token.PNG)


`**Rember to save the value of token`(it will show only once)

--------------------------------------------------------

# Add GitHub Server in Jenkins

**goto Jenkins Web GUI(example: http://23.236.114.227:8080)**

![](/assets/jenkins-github/2.add-github-server-in-jenkins.png)

# Use github token in Jenkins

- Create a Credential
  - kind: "Secret text"
  - Secret: `<github personal access token>`

![](/assets/jenkins-github/3.use-personal-token-in-jenkins.png)

# Test github token in Jenkins
![](/assets/jenkins-github/4.test-github-connection.png)

