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
        stage('todos-api Analysis ') {
            agent any
            when {
                changeset "**/todos-api/*.*"
                beforeAgent true
            }
            steps {
                dir('todos-api'){
                    nodejs(nodeJSInstallationName: 'nodejs'){
                    sh 'npm install'
                             script {
                                def scannerHome = tool 'SonarQube';
                                withSonarQubeEnv('sonar') {
                                sh "${tool("SonarQube")}/bin/sonar-scanner -Dsonar.projectKey=reactapp -Dsonar.projectName=reactapp"
                                }
                             }
                    }
                }
            }
        }
        stage('Sonarqube quality gate') {
            agent any
            when {
                changeset "**/todos-api/*.*"
                beforeAgent true
            } 
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build auth-api ') {
            agent any
            when {
                changeset "**/auth-api/*.*"
                beforeAgent true
            }
            steps {
                dir('auth-api and Analysis'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/auth-api .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/auth-api'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/auth-api'
                    sh 'docker logout'
                }
            }
        }
        stage('Build frontend ') {
            agent any
            when {
                changeset "**/frontend/*.*"
                beforeAgent true
            }
            steps {
                dir('frontend'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/frontend .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/frontend'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/frontend'
                    sh 'docker logout'
                }
            }
        }
        stage('Build log-message-processor ') {
            agent any
            when {
                changeset "**/log-message-processor/*.*"
                beforeAgent true
            }
            steps {
                dir('log-message-processor'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/log-message-processor .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/log-message-processor'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/log-message-processor'
                    sh 'docker logout'
                }
            }
        }
        stage('Build todos-api ') {
            agent any
            when {
                changeset "**/todos-api/*.*"
                beforeAgent true
            }
            steps {
                dir('todos-api'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/todos-api .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/todos-api'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/todos-api'
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
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/users-api .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/users-api'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/users-api'
                    sh 'docker logout'
                }
            }
        }
    //    stage('deplou on k8s'){
           // steps {
          //    sshagent(['k8s']) {                     
            //            sh 'ssh root@24.199.98.234 kubectl apply -f .'    
         //}
         //   }
      //  }
    }
}
