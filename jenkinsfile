pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm // add ur git repo 
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
