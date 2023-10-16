pipeline {
  agent { label 'debian_node' }
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
