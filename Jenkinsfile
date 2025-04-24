pipeline {
    agent any
    tools{
        maven 'maven_3_9_9'
    }
    stages{
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/AMT10/spring-boot-docker.git']])
            }
        }
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AMT10/spring-boot-docker.git']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t amitghatage1011/spring-boot-docker .'
                }
            }
        }
        stage('Push Image To Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'DOCKER_HUB_PASSWORD')])
                        {
                            bat "docker login -u amitghatage1011 -p %DOCKER_HUB_PASSWORD%"
                         }
                        bat 'docker push amitghatage1011/spring-boot-docker'
                    }
            }
        }

    }
}