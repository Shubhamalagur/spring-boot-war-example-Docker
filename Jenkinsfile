pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages {
        stage('SCM checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Shubhamalagur/spring-boot-war-example-Docker.git']])
            }
         }
         stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage("docker build and deploy")
            {
            steps{
                    withCredentials([string(credentialsId: 'dockerhub2', variable: 'docker_password')]) 
                    {
                      sh '''
                        docker build -t shubham177501/demo-1:${VERSION} .
                        docker login -u shubham177501 -p $docker_password
                        docker push shubham177501/demo-1:${VERSION}
                        docker rmi shubham177501/demo-1:${VERSION}
                    '''
                }
            }
        }
        }
    }
