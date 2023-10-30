pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'bb91983a-0f2a-4ab5-bc49-3f1c44620be4', url: 'https://github.com/shubhamasthana507/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t shubhamasthana507/devops-integration .'
                }
            }
        }
        stage('push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u shubhamasthana507 -p ${dockerhubpwd}'
            }
                sh 'docker push shubhamasthana507/devops-integration'
                }
            }
        }
    }
}