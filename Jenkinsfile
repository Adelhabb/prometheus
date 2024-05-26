pipeline {
    agent any
        environment {
        PM_API_URL = "https://192.168.217.128:8006/api2/json"
        PM_USER = "root"
        PM_PASSWORD = "adminprox"
             }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Test GitHub Connection') {
            steps {
                script {
                    def gitRepoUrl = 'https://github.com/Adelhabb/prometheus.git'
                    def gitTestDir = 'test-git-repo'
                    git(url: gitRepoUrl, branch: 'main', changelog: false, poll: false, dir: gitTestDir)
                    echo "Connection to GitHub repository successful"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose down --remove-orphans'
                sh 'docker-compose up -d'
            }
        }
    }
}
