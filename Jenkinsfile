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

                  stage('Build') {
                      steps {
                          script {
                              // Generate the JAR file
                              sh './gradlew jar'

                              // Generate the documentation
                              sh './gradlew javadoc'
                          }
                      }
                      post {
                          success {
                              // Archive the generated JAR and documentation
                              archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
                              archiveArtifacts artifacts: 'build/docs/javadoc/**/*', fingerprint: true
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