pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './gradlew test'
                junit '**/build/test-results/test/*.xml' // Adjust path based on your project structure
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