pipeline {
    agent any

    triggers {
        pollSCM('*/5 * * * *')
    }

    stages {
        stage('Compile') {
            steps {
                gradlew('clean', 'classes')
            }
        }

        stage('Long-running Verification') {
/*             environment {
                SONAR_LOGIN = credentials('SONARCLOUD_TOKEN')
            } */
            parallel {
                stage('Integration Tests') {
                    steps {
                        gradlew('integrationTest')
                    }
                }
                stage('Code Analysis') {
                    steps {
                        gradlew('sonarqube')
                    }
                }
            }
        }
        stage('Assemble') {
            steps {
                gradlew('assemble')
                stash includes: '**/build/libs/*.war', name: 'app'
            }
        }
        stage('Promotion') {
            steps {
                timeout(time: 1, unit:'DAYS') {
                    input 'Deploy to Production?'
                }
            }
        }
        stage('Deploy to Production') {
/*             environment {
                HEROKU_API_KEY = credentials('HEROKU_API_KEY')
            } */
            steps {
                unstash 'app'
                gradlew('deployHeroku')
            }
        }
    }
    post {
        failure {
            mail to: 'didwltjs324@gmail.com', subject: 'Build failed', body: 'Please fix!'
        }
    }
}

def gradlew(String... args) {
    sh "./gradlew ${args.join(' ')} -s"
}