pipeline {
    agent any
        environment {
        PM_API_URL = "https://192.168.217.128:8006/api2/json"
        PM_USER = "root"
        PM_PASSWORD = "adminprox"
             }
stages {
        stage('Test GitHub Connection') {
            steps {
                script {
                    def gitUrl = 'https://github.com/Adelhabb/promethious.git'
                    // Checkout the GitHub repository using configured credentials
                    checkout([$class: 'GitSCM',
                              branches: [[name: '*/main']],
                              doGenerateSubmoduleConfigurations: false,
                              extensions: [[$class: 'CloneOption', depth: 1, noTags: false, reference: '', shallow: true]],
                              userRemoteConfigs: [[url: gitUrl]]])
                    echo "Connection to GitHub repository successful"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}

