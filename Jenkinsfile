pipeline {
  agent { label 'kubeslave' }
  stages {
    stage('Prepare workspace') {
      steps {
        script {
          projectInfo = readYaml (file: './project.yaml')
          currentBuild.displayName = "${projectInfo.VERSION}-${env.BRANCH_NAME}-${GIT_COMMIT[0..5]}"
        } 
      }
    }
    stage('Build and Dockerize') {
      steps{
        container('docker') {
          script {
            docker.withRegistry('', 'dockerjenkins') {
              dockerImage = docker.build("${projectInfo.DOCKER_REPOSITORY}/${projectInfo.NAME}:${projectInfo.VERSION}-${env.BRANCH_NAME}-${GIT_COMMIT[0..5]}")
              dockerImage.push()
            }
          }
        }
      }
    }
  }
}
