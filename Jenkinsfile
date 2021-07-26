pipeline {
    agent any

    triggers{
        bitbucketPush()
    }

    stages {
        stage ('Test & Build Artifact') {
            agent {
                docker {
                    image 'openjdk:11'
                    args '-v "$PWD":/app'
                    reuseNode true
                }
            }
            steps {
                sh './gradlew clean build'
            }
        }
        stage ('Build & Push docker image') {
            steps {
                withDockerRegistry(url: 'https://index.docker.io/v1/') {
                    sh 'docker push turkogluc/spring-jenkins-demo'
                }
            }
        }
    }
}