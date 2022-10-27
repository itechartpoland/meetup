pipeline {
  agent { label 'kubeslave' }
  stages {
    stage('Build and Dockerize') {
      steps{
        container('builder') {
          script {
              sh "docker pull docker.io/eclipse-temurin:17-jdk-jammy"
              sh "docker build . -t itechartpoland/meetup-java-app:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
              sh "docker push itechartpoland/meetup-java-app:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
          }
        }
      }
    }
  }
}
