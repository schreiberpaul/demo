pipeline {
    agent {
        node {
            label 'built-in'
        }
    }
    steps {
        stage('SCM') {
            checkout scm
        }
        stage('SonarQube Analysis') {
            withSonarQubeEnv() {
            sh ".mvnw clean verify sonar:sonar -Dsonar.projectKey=demo -Dsonar.projectName='demo'"
            }
        }
    }
}
