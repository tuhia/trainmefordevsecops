pipeline {
    agent {
  label 'docker'
}

    stages {
        stage('Git Clone') {
            steps {
                    checkout scmGit(branches: [[name: 'email-notification']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/tuhia/trainmefordevsecops.git']])

                }
        }
        stage('SAST') {
            steps {
                    sh ''
                }
            }
        stage('Build and Tag ') {
            steps {
                script {
                     app = docker.build("tuhia/snake:${env.BUILD_ID}")
                }
                }
        }
        stage('Image and Vulnerabilty Scan ') {
            steps {
                     sh ''
                }
        }
        stage('Post to Docker Hub  ') {
            steps {
                script {
                docker.withRegistry('https://registry.hub.docker.com','dockerhub') {
                    app.push("${env.BUILD_ID}")
                    }
                }
                }
        }
        stage('Pull image Server  ') {
            steps {
                     sh 'docker compose down'
                     sh 'docker compose up -d'
                
                }
        }
        stage('DAAST  ') {
            steps {
                     sh ''
                }
        }
    }
}
