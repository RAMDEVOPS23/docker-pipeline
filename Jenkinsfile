pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('ramdocker611-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/RAMDEVOPS23/docker-pipeline.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ramdocker611/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push ramdocker611/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

