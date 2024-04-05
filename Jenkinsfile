//create a pipeline job for maven project which will create a Docker image and push it to Docker Hub repository.
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    def mvnHome = tool 'M3'
                    def mvnCMD = "${mvnHome}/bin/mvn"
                    sh "${mvnCMD} clean package"
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("maven-docker-image:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("maven-docker-image:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}

 Step 4:  Now, run the Jenkins pipeline job and check the console output.
 Step 5:  Once the Jenkins pipeline job is completed, check the Docker Hub repository.
 Step 6:  You can see the Docker image is pushed to the Docker Hub repository.
 Summary:
 In this article, we have learned how to create a Jenkins pipeline job for a maven project which will create a Docker image and push it to the Docker Hub repository.
 You can also refer to the below articles to know more about Jenkins.

 Jenkins Pipeline for Continuous Integration and Continuous Deployment
 Jenkins Pipeline for Continuous Integration and Continuous Deployment
 Jenkins Pipeline for Continuous Integration and Continuous Deployment
 Jenkins Pipeline for Continuous Integration and Continuous Deployment

 I hope you like this article. Please provide your valuable feedback and suggestions in the comment section.
 Share this: Tweet WhatsApp WhatsApp Email Email
 Related
 Post was not sent - check your email addresses!
 Email check failed, please try again
 Sorry, yourjson cannot share posts by email.