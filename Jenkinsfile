pipeline {
  agent { label 'dev_server' }
  stages {
    stage('Tooling versions') {
      steps {
        sh '''
          docker --version
          docker compose version
        '''
      }
    }
  }
}
