pipeline {
  agent { label 'kubeslave' }
  stages {
    stage('Build and Dockerize') {
      steps{
        container('builder') {
          script {
              sh "docker pull docker.io/eclipse-temurin:17-jdk-jammy"
              sh "docker build . -t itechartpoland/meetup-java-app:1.0.0-${env.BRANCH_NAME}"
              sh "docker push itechartpoland/meetup-java-app:1.0.0-${env.BRANCH_NAME}"
          }
        }
      }
    }
  }
}
