pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                script{
                    bat './gradlew test'
                }
            }
            post {
                always {
                    junit 'build/test-results/test/*.xml'
                    cucumber 'reports/example-report.json'
                }
            }
        }

        stage('SonarQube') {
            steps {
                bat './gradlew sonar'
            }
        }

        stage('Hello World') {
            steps {
                echo 'Hello World'
            }
        }
    }
}