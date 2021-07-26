pipeline {
    agent any
    stages {
        stage('Build gradle') {
            steps {
                sh './gradlew build'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t mbox:latest .'
            }
        }
    }
}