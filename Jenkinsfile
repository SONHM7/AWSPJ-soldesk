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

        stage('tag'){
            steps{
                sh 'docker tag mbox:latest public.ecr.aws/d0u4r1r6/jenkins:latest'
            }
        }

        stage('push'){
            steps{
                sh 'docker push public.ecr.aws/d0u4r1r6/jenkins:latest'
            }
        }
    }
}