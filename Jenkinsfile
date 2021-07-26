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
            sh 'aws ecr-public get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin public.ecr.aws/d0u4r1r6'
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