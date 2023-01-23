pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker-hub-repo')
    }
    stages {
         stage('Checkout'){
            agent any
            steps{
                git url: 'https://github.com/naiveskill/devops_cred.git', branch: 'main'
            }
        }
        stage('Init'){
            agent any
            steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build auth-api') {
            agent any
            when {
                changeset "**/auth-api/*.*"
                beforeAgent true
            }
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
            agent any
            when {
                changeset "**/frontend/*.*"
                beforeAgent true
            }
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
            agent any
            when {
                changeset "**/log-message-processor/*.*"
                beforeAgent true
            }
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
            agent any
            when {
                changeset "**/todos-api/*.*"
                beforeAgent true
            }
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
            agent any
            when {
                changeset "**/users-api/*.*"
                beforeAgent true
            }
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
