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

  }
}
