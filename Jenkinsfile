pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Adelhabb/prometheus.git'
            }
        }
        stage('List Files') {
            steps {
                script {
                    sh 'pwd'  // Affiche le répertoire de travail actuel
                    sh 'ls -l'  // Liste les fichiers dans le répertoire actuel
                }
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
                        sh 'docker-compose -f docker-compose.yml config'
                        sh 'docker-compose -f docker-compose.yml up -d --remove-orphans'
                    } catch (e) {
                        echo 'Docker Compose not found or not executable'
                        error 'Stopping the pipeline'
                    }
                }
            }
        }
    }
}
