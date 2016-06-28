#Use Case

1. Project source code is hosted on GitHub
2. Jenkins server(with hyper cli installed) is hosted on Hyper_
3. Use Jenkins job to build(pull,make,test and upload) project in container which hosted on Hyper_
4. Start Jenkins build when a change is pushed to GitHub
5. When Jenkins start build, a new Hyper_ container will be created
6. The whole build process(`pull code-> unit-test-> make-> integration-test-> upload`) will be done in this Hyper_ container
7. If Jenkins build successfully, the result(binary archive file) will be uploaded to AWS S3
8. Finally, the Hyper_ container will be destroy