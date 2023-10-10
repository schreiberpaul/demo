pipeline {
    agent {
        node {
            label 'built-in'
        }
    }
    stages {
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv() {
                sh ".mvnw clean verify sonar:sonar -Dsonar.projectKey=demo -Dsonar.projectName='demo'"
                }
            }
        }
    }
}
