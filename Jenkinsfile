pipeline {
    agent any
    tools{
        maven 'maven_3_9_0'
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages{
        stage('Build Maven'){
            steps{
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Francis-Nwachukwu/devops-automation.git']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
          steps{
            script{
                dockerImage = docker.build("francisnwachukwu100/devops-integration:latest")
            }
          }
        }
        stage('Push image') {
            steps{
                script{
                    withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                        dockerImage.push()
                    }
                }
            }
           
        }
    }
}