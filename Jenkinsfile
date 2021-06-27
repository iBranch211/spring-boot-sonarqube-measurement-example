
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
         stage('Code Quality Check via SonarQube') {
           steps {
                script {
                 def scannerHome = tool 'sonarqube';
                 withSonarQubeEnv("sonarqube") {
                   sh "${tool("sonarqube")}/bin/sonar-scanner"
                }
             }
           }
         }

       stage('Build') {
          steps {
            sh "mvn jib:dockerBuild"
          }
       }

       stage('Docker Publish') {
          steps {
            withDockerRegistry([credentialsId: "${IMAGE_REGISTRY_CREDENTIAL}", url: ""]) {
              sh "docker push ${IMAGE_REGISTRY}:${IMAGE_VERSION}"
            }
          }
       }

       stage('Deploy Docker-compose') {
         steps {
           sh "docker-compose pull"
           sh "docker-compose up -d --remove-orphans"
         }
       }
    }
}