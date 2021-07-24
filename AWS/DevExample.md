## AWS has a lot of images ready to go.  Reuse their work.  

For a broadly-reusable general development docker file model, see the "[Ubuntu Standard 5.0](https://github.com/aws/aws-codebuild-docker-images/tree/master/ubuntu/standard/5.0)" from AWS.  
This seems like it would be useful for a broad spectrum of application development use cases.  
And if expense management and runtime speed are high priorities, it also seems like an easy starting point for building your own optimized image.  
Copy the dockerfile and remove the language/runtime/build tooling support that you don't need, and generate a lighter container.  
See: [https://github.com/aws/aws-codebuild-docker-images/tree/master/ubuntu/standard/5.0](https://github.com/aws/aws-codebuild-docker-images/tree/master/ubuntu/standard/5.0)  
July 2021 runtimes:  
* java: Java version 8 and 11  
* golang: Go version 1.15.6  
* python: Python version 3.7.10, 3.8.8, and 3.9.2  
* php: PHP version 7.3.25, 7.4.13, and 8.0.0  
* ruby: Ruby version 2.6 and 2.7  
* nodejs: Node.js version 12 and 14  
* dotnet: .NET version 3.1.404 and 5.0.202  
 
The docker file shows that in July 2021 it also has installed:  
* PowerShell core 7.1.0  
* Python modules: pip setuptools wheel aws-sam-cli boto3 pipenv virtualenv  
* Ant 1.10.9  
* Maven 3.6.3  
* Gradle 5.6.4 & 6.7  
