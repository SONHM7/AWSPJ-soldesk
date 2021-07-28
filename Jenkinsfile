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

        stage('login'){
            steps{
                sh 'aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 783845918471.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins'
            }
        }

        stage('tag'){
            steps{
                sh 'docker tag mbox:latest 783845918471.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins:latest'
            }
        }

        stage('push'){
            steps{
                sh 'docker push 783845918471.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins:latest'
            }
        }
    }
}