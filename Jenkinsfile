node {

    stages {
        stage('Build gradle') {
            sh './gradlew build'
        }

        stage('Build docker image') {
            sh 'docker build -t $registry:latest .'
        }
      }
}