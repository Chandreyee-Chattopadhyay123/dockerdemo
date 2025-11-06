pipeline {
   agent any
    
    stages {
        stage('Checkout GitHub repo') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Chandreyee-Chattopadhyay123/dockerdemo.git']])
            }
        }
        stage('Build and Tag Docker Image') {
            steps {
                script {
                    sh 'docker build . -t hellodocker'
                    sh 'docker tag hellodocker Chandreyee-Chattopadhyay123/learning'
                }
            }
        }    
        stage('Push the Docker Image to DockerHUb') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
                    sh 'docker login -u chandreyee.chattopadhyay.cse26@heritageit.edu.in -p ${docker_hub}'
}
                    sh 'docker push Chandreyee-Chattopadhyay123/learning'
                }
            }
        }
        
        stage('Deploy deployment and service file') {
            steps {
                script {
                    kubernetesDeploy configs: 'deploymentsvc.yaml', kubeconfigId: 'k8_auth'
                }
            }
        } 
    }      
}
