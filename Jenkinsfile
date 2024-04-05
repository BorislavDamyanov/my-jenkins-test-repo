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

