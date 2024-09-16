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
               sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
        }
        stage('test'){
            steps{
            sh 'mvn surefire-report:report'
            }
        }
        // stage('SonarQube analysis') {
        //     environment{
        //     scannerHome = tool 'Awsdevopspro-Sonar-Scanner'}
        //     steps{
        //     withSonarQubeEnv('Awsdevopspro-SonarQube-Server') 
        //     {// If you have configured more than one global server connection, you can specify its name
        //     sh "${scannerHome}/bin/sonar-scanner"
        //     }
        //     }
        // }

        stage('SonarQube analysis') {
            tools {
                jdk "jdk17" // the name you have given the JDK installation in Global Tool Configuration
            }
            environment {
                scannerHome = tool 'Awsdevopspro-Sonar-Scanner' // the name you have given the Sonar Scanner (in Global Tool Configuration)
            }
            steps {
                withSonarQubeEnv(installationName: 'Awsdevopspro-SonarQube-Server') {
                    sh "${scannerHome}/bin/sonar-scanner -X"
                }
            }
        }
        stage("Quality Gate"){
            steps{
            timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
                qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                if (qg.status != 'OK') {
                error "Pipeline aborted due to quality gate failure: ${qg.status}"
                }
                }
  }
}
    }
}
