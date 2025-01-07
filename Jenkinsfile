pipeline {
    agent any

    environment {
        SLACK_CHANNEL = '#chat'  // Replace with your channel
    }

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
                              bat './gradlew jar'

                              // Generate the documentation
                              bat './gradlew javadoc'
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

        stage('Deploy') {
            steps {
                echo 'Hello World'
            }
        }
    }

    post {
        success {

              mail(
                  to: 'ls_yekene@esi.dz',
                  subject: 'Deployment Success',
                  body: 'The deployment was successful.'
              )
            slackSend(
                channel: SLACK_CHANNEL,
                color: 'good',
                message: "✅ Build #${env.BUILD_NUMBER} completed successfully!\nBuild URL: ${env.BUILD_URL}"
            )
        }
        failure {
            slackSend(
                channel: SLACK_CHANNEL,
                color: 'danger',
                message: "❌ Build #${env.BUILD_NUMBER} failed!\nBuild URL: ${env.BUILD_URL}"
            )
        }
        unstable {
            slackSend(
                channel: SLACK_CHANNEL,
                color: 'warning',
                message: "⚠️ Build #${env.BUILD_NUMBER} is unstable!\nBuild URL: ${env.BUILD_URL}"
            )
        }
    }
}