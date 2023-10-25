pipeline {
  agent { label 'debian_node_ecs' }
  environment {
    DOCKER_HUB_CREDS = credentials('zaklukasz-docker-hub')
    AWS_CREDS = credentials('zaklukasz-aws-creds')
  }
    stages { 
        stage('Get Code') {
            steps {
                fileOperations([folderCreateOperation('basic')])
                dir('basic') {
                    git credentialsId: 'planner-gitlab', url: 'https://gitlab.iwq.local/developers/planner.git'
                    }
                }
            }
          stage('Get build scripts') {
            steps {
                fileOperations([folderCreateOperation('buildscripts')])
                dir('buildscripts') {
                    git credentialsId: 'planner-gitlab', url: 'https://gitlab.iwq.local/developers/BuildScripts.git'
                    }
                }
            }
          stage("Run Composer scripts"){
            steps {
                    sh 'git config --global http.sslVerify false'
                    dir('basic') {
                        sh 'composer install && composer update'
                    }      
                    input('xxx')
              
            }
        }  
  }
}
