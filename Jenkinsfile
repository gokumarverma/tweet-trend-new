pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment{
        PATH="/usr/bin/mvn:$PATH"
    }
    stages {
        stage('build') {
            steps {
               sh 'mvn clean deploy'
            }
        }
    }
}
