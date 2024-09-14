pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment{
        PATH="/opt/maven/bin:$PATH"
    }
    stages {
        stage('build') {
            steps {
               sh 'mvn clean deploy'
            }
        }

        stage('SonarQube analysis') {
            environment{
                ScannerHome= tool SonarScanner
            }
            steps{
            withSonarQubeEnv('SonarQube') { 
            // You can override the credential to be used, If you have configured more than one global server connection, you can specify the corresponding SonarQube installation name configured in Jenkins
            sh "${SonarQube}/bin/SonarScanner"
            }
            }
        }
}
        }
