pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-bhargavchamp')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Bhargav-LNSN/docker-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t bhargavchamp/docker_practice:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push bhargavchamp/docker_practice:$BUILD_NUMBER'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull bhargavchamp/docker_practice:$BUILD_NUMBER'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 443:80 bhargavchamp/docker_practice:$BUILD_NUMBER'
            }
        }   
        
}
post {
        always {
            sh 'docker logout'
        }
    }
}

