pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('fetch code') {
            steps {
                git branch: 'main', url: 'https://github.com/gokumarverma/tweet-trend-new.git'
            }
        }
    }
}
