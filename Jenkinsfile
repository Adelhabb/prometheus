pipeline {
    agent any
    stages {
        stage('Check Docker Compose') {
            steps {
                sh 'docker compose version || { echo "Docker Compose n\'est pas installé"; exit 1; }'
            }
        }
        stage('Déployer') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
