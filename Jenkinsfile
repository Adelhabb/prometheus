pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_VERSION = '1.29.2'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Adelhabb/prometheus.git' // Mettez ici l'URL de votre dépôt
            }
        }

        stage('Install Docker Compose') {
            steps {
                sh '''
                    if ! [ -x "$(command -v docker-compose)" ]; then
                      curl -L "https://github.com/docker/compose/releases/download/$DOCKER_COMPOSE_VERSION/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
                      chmod +x /usr/local/bin/docker-compose
                    fi
                '''
            }
        }

        stage('Deploy Services') {
            steps {
                sh 'docker-compose down --remove-orphans'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            script {
                echo "Cleaning up dangling images"
                sh 'docker image prune -f'
            }
        }
    }
}
