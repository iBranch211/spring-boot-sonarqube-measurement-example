
pipeline {
    agent any
    environment {
        IMAGE_REGISTRY = 'suayb/golang-echo-graphql-example'
        IMAGE_VERSION = '1.0.0'
        IMAGE_REGISTRY_CREDENTIAL = 'dockerhubcreds'
    }
    stages {
        stage('SonarQube analysis') {
            steps {
                script {
                  scannerHome = tool 'sonarqube'
                }
                withSonarQubeEnv('sonarqube') {
                  sh "${scannerHome}/bin/sonar-scanner \
                  -D sonar.login=admin \
                  -D sonar.password=root \
                  -D sonar.projectKey=spring-boot-sonarqube-measurement-example \
                  -D sonar.exclusions=vendor/**,resources/**,**/*.java \
                  -D sonar.host.url=http://192.168.1.35:9000/"
                }
            }
        }
    }
}