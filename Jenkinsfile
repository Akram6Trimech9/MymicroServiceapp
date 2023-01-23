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
        stage('Build auth-api and Analysis') {
            agent any
            when {
                changeset "**/auth-api/*.*"
                beforeAgent true
            }
            steps {
                dir('auth-api and an'){
                    sh "sonar-scanner-cli -Dsonar.projectKey=go_project -Dsonar.sources=auth-api -Dsonar.language=go"
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/auth-api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/auth-api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/auth-api:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build frontend and Analysis') {
            agent any
            when {
                changeset "**/frontend/*.*"
                beforeAgent true
            }
            steps {
                dir('frontend'){
                    sh "sonar-scanner-cli -Dsonar.projectKey=viewjs_project -Dsonar.sources=frontend -Dsonar.language=javascript"
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/frontend$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build log-message-processor and Analysis') {
            agent any
            when {
                changeset "**/log-message-processor/*.*"
                beforeAgent true
            }
            steps {
                dir('log-message-processor'){
                    sh "sonar-scanner -Dsonar.projectKey=node_project -Dsonar.sources=log-message-processor -Dsonar.language=javascript"
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/log-message-processor:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/log-message-processor:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/log-message-processor:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build todos-api and Analysis') {
            agent any
            when {
                changeset "**/todos-api/*.*"
                beforeAgent true
            }
            steps {
                dir('todos-api'){
                    sh "sonar-scanner -Dsonar.projectKey=node_project -Dsonar.sources=todos-api -Dsonar.language=javascript"
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/todos-api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/todos-api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/todos-api:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build users-api Analysis ') {
            agent any
            when {
                changeset "**/users-api/*.*"
                beforeAgent true
            }
            steps {
                dir('users-api'){
                    sh "sonar-scanner-cli -Dsonar.projectKey=java_project -Dsonar.sources=users-api -Dsonar.language=java"
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/users-api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/users-api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/users-api:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
    }
}
