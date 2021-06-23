
pipeline {
   agent {
          docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            reuseNode true
          }
   }
    environment {
        IMAGE_REGISTRY = 'dockerhub.detaysoft.com/das/das-api'
        IMAGE_VERSION = 'latest'
        IMAGE_REGISTRY_CREDENTIAL = 'dockerhubcreds'
        DOCKER_REGISTRY_URL = ""
    }
    stages {
        stage('Testing') {
           steps {
             sh "mvn verify"
           }
        }

        stage('SonarQube Analysis') {
           steps {
             sh "mvn initialize sonar:sonar"
           }
        }

       stage('Build') {
          steps {
            sh "mvn jib:dockerBuild"
          }
       }
    }
}