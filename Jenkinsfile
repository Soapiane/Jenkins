pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                script{
                    sh './gradlew test'
                }
            }
        }

        stage('SonarQube') {
            steps {
                sh './gradlew sonar'
            }
        }

        stage('Hello World') {
            steps {
                echo 'Hello World'
            }
        }
    }
}