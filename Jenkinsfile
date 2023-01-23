pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker-hub-repo')
    }
    stages {
         stage('Checkout'){
            agent any
            steps{
                git url: 'https://github.com/Akram6Trimech9/MymicroServiceapp.git', branch: 'main'
            }
        }
        stage('Init'){
            agent any
            steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build auth-api') {            
            steps {
                dir('auth-api'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/auth-api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/auth-api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/auth-api:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build frontend') {
            steps {
                dir('frontend'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/frontend$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build log-message-processor') {
            steps {
                dir('log-message-processor'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/log-message-processor:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/log-message-processor:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/log-message-processor:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build todos-api') {
            steps {
                dir('todos-api'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/todos-api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/todos-api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/todos-api:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build users-api') {
            steps {
                dir('users-api'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/users-api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/users-api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/users-api:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
    }
}
