pipeline {
  agent { label 'debian_node' }
  environment {
    DOCKER_HUB_CREDS = credentials('zaklukasz-docker-hub')
    AWS_CREDS = credentials('zaklukasz-aws-creds')
  }
  stages {
    stage('Tooling versions') {
      steps {
        sh '''
          docker --version
          docker-compose version
        '''
      }
    }
    stage('Build') {
      steps {
        sh 'docker-context use default'
        sh 'docker-compose build'
        sh 'docker-compose push'
      }
    }
    stage('Deploy') {
      steps {
        sh 'docker context use myecscontext'
        sh 'docker-compose up'
        sh 'docker-compose ps --format json'
      }
    }
  }
}