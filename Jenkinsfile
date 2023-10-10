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
                withSonarQubeEnv(installationName: 'SonarQube1') {
                sh ".mvnw clean verify sonar:sonar -Dsonar.projectKey=demo -Dsonar.projectName='demo'"
                }
            }
        }
    }
}
