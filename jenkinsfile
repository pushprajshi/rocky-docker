pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/pushprajshi/rocky-docker.git']]
                ])
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t rocky-docker:latest .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker rm -f rocky || true'
                sh 'docker run -d --name rocky -p 8080:80 rocky-docker:latest'
            }
        }
        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
