//create a pipeline job for maven project which will create a Docker image and push it to Docker Hub repository.
pipeline {
    agent any
    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "${dockerHome}/bin:${mavenHome}/bin:${PATH}"
    }
    stages {
         stage('Checkout') {
                steps {
                   sh 'docker --version'
                   sh 'mvn --version'
                }
            }

        stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('Docker Build') {
            steps {
                script {
                   dockerImage = docker.build("boris1030/my-jenkins-test-repo:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                        dockerImage.push();
                        dockerImage.push("latest");
                    }
                }
            }
        }
    }
}

