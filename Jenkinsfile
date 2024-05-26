pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Adelhabb/prometheus.git'
            }
        }
        stage('Test GitHub Connection') {
            steps {
                script {
                    try {
                        checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],
                                       userRemoteConfigs: [[url: 'https://github.com/Adelhabb/promethious.git']]]
                        echo 'Connection to GitHub repository successful'
                    } catch (e) {
                        echo 'Failed to connect to GitHub repository'
                        error 'Stopping the pipeline'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    try {
                        sh 'docker-compose --version'
                        sh 'docker-compose up -d'
                    } catch (e) {
                        echo 'Docker Compose not found'
                        error 'Stopping the pipeline'
                    }
                }
            }
        }
    }
}
