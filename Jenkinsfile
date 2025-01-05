pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                script{
                    bat './gradlew test'
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