pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                script{
                    bat './gradlew test'
                }
                post {
                    always {
                        junit 'build/test-results/test/*.xml'
                        cucumber 'build/reports/cucumber/*.json'
                    }
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