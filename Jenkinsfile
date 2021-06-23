
pipeline {
   agent {
          docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v $HOME/.m2:/root/.m2'
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
        stage('SonarQube Analysis') {
           steps {
             sh "mvn verify sonar:sonar"
           }
        }

       stage('Build') {
          steps {
            sh "mvn compile jib:dockerBuild"
          }
       }
    }
}