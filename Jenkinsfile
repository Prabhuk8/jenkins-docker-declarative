pipeline {
    agent any
    tools{
        maven 'Maven3'
    }
    stages{
        stage("Build maven project"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Prabhuk8/jenkins-docker-declarative']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t prabhusujan/docker-jenkins-declarative .'
                }
            }
        }
        stage('Docker push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubsecretpwd', variable: 'dockerhubsecretpwd')]) {
                    sh 'docker login -u prabhusujan -p ${dockerhubsecretpwd}'
}
                    sh 'docker push prabhusujan/docker-jenkins-declarative'
                }
            }
        }
    }
}
