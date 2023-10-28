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
    stage('Run Composer scripts') {
      steps {
        sh 'git config --global http.sslVerify false'
        dir('basic') {
          sh 'composer install && composer update'
        }
      //input('xxx')
      }
    }
    stage('Get Dockerfile') {
      steps {
        fileOperations([folderCreateOperation('docker_file')])
        dir('docker_file') {
          git credentialsId: 'planner-gitlab', url: 'https://gitlab.iwq.local/developers/devops/iwq_basic_docker.git'
        }
      }
    }
    stage('Tar code') {
      steps {
        dir('basic') {
          /* groovylint-disable-next-line LineLength */
          sh 'tar -czvf /home/jenkins/workspace/aws-web-app-docker-compose/basic.tar /home/jenkins/workspace/aws-web-app-docker-compose/basic'
        }
      }
    }
    stage('Build Dockerfile') {
      steps {
        dir('docker_file') {
          sh 'pwd'
          sh 'docker build --build-arg KATALOG_TAR=/home/jenkins/workspace/aws-web-app-docker-compose/basic.tar -t iwq_basic:${Version} . '
        //-f ./workspace/aws-web-app-docker-compose/docker_file/Dockerfile
        }
      }
    }
    }
}
