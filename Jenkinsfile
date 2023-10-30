pipeline {
  agent { label 'debian_node_ecs' }
  environment {
    DOCKER_HUB_CREDS = credentials('zaklukasz-docker-hub')
    AWS_CREDS = credentials('zaklukasz-aws-creds')
  }
    stages {
        stage('Get Code') {
      steps {
        fileOperations([folderCreateOperation('iwqbasic/basic_code')])
        dir('iwqbasic/basic_code') {
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
        dir('iwqbasic/basic_code') {
          sh 'composer install && composer update'
        }
      //input('xxx')
      }
    }
    stage('Get Dockerfile') {
      steps {
        //fileOperations([folderCreateOperation('docker_file')])
        dir('iwqbasic') {
          git credentialsId: 'planner-gitlab', url: 'https://gitlab.iwq.local/developers/devops/iwq_basic_docker.git'
        }
      }
    }
    stage('Tar code') {
      steps {
        dir('iwqbasic') {
          /* groovylint-disable-next-line LineLength */
          //sh 'tar -czvf /home/jenkins/workspace/aws-web-app-docker-compose/basic.tar /home/jenkins/workspace/aws-web-app-docker-compose/basic'
        }
      }
    }
    stage('Build Dockerfile') {
      steps {
        dir('iwqbasic') {
          sh 'pwd'
          sh 'docker build -t iwq_basic:${Version} .'
          //sh 'docker buildx build --build-context project=/home/jenkins/workspace/aws-web-app-docker-compose/ .'
        //-f ./workspace/aws-web-app-docker-compose/docker_file/Dockerfile
        }
      }
    }
    }
}
