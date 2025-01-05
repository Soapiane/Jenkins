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
                withSonarQubeEnv('sonar') { // Replace 'SonarQube' with the name of your configured SonarQube server in Jenkins
                    bat './gradlew sonar '
                }
            }
        }

        stage('Code Quality') {
             steps {
                 script {
                     def qualityGate = waitForQualityGate() // Wait for SonarQube's analysis result
//                      if (qualityGate.status != 'OK') {
//                          error "Pipeline failed due to Quality Gate failure: ${qualityGate.status}"
//                      }
                 }
             }
         }

        stage('Hello World') {
            steps {
                echo 'Hello World'
            }
        }
    }
}