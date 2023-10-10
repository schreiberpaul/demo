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
                sh "./mvnw clean verify sonar:sonar -Dsonar.projectKey=demo -Dsonar.projectName='demo'"
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
                    stopBuild: true,
                    odcInstallation: 'OWASP Dependency-Check'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml',
                failedTotalCritical: 0
            }
        }
    }
}
