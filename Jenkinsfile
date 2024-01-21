pipeline {
    agent {
        node {
            label 'built-in'
        }
    }
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv(installationName: 'SonarQube1') {
                sh "./mvnw clean verify sonar:sonar -Dsonar.projectKey=webgoat -Dsonar.projectName='webgoat'"
                }
            }
        }
        stage('OWASP Dependency Check') {
            steps {
            
                dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'XML'
                    -f 'HTML'
                    -prettyPrint
                    --failOnCVSS 0''',
                    odcInstallation: 'OWASP Dependency-Check'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml',
                failedTotalCritical: 0
            }
        }
    }
}
