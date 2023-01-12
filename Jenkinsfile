pipeline {
    agent any
    tools{
        maven 'maven_3_8_7'
    }
    stages{
        stage('Build Maven'){
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/imadberoual/devops-automation']])
            sh 'mvn clean install'
        }
        stage('Build docker image'){
            sh 'docker build -t imdbr/devops-integration .'
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                     sh 'docker login -u imdbr -p ${dockerhubpwd}'
}
                    sh 'docker push imdbr/devops-integration'
                }
            }
        }
    }
}