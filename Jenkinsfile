node {

    stages {
        stage('Build gradle') {
        sh './gradlew build'
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t $registry:latest .'
            }
        }
      }
}