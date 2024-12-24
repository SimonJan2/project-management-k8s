pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        SERVER_IMAGE = 'simonjan2/project-management:server'
        CLIENT_IMAGE = 'simonjan2/project-management:client'
    }
    
    stages {
        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        
        stage('Build Server Image') {
            steps {
                dir('server') {
                    sh 'docker build -t ${SERVER_IMAGE} .'
                }
            }
        }
        
        stage('Build Client Image') {
            steps {
                dir('client') {
                    sh 'docker build -t ${CLIENT_IMAGE} .'
                }
            }
        }
        
        stage('Push Server Image') {
            steps {
                sh 'docker push ${SERVER_IMAGE}'
            }
        }
        
        stage('Push Client Image') {
            steps {
                sh 'docker push ${CLIENT_IMAGE}'
            }
        }
    }
    
    post {
        always {
            sh 'docker logout'
        }
    }
}
