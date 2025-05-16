pipeline {
    agent any

    environment {
        PROJECT_NAME = "plantcare_ci"
        COMPOSE_FILE = "docker-compose.yaml"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/ZeshanDev1/Plant-Care-Automation-main.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh "docker-compose -p ${PROJECT_NAME} -f ${COMPOSE_FILE} build || exit 1"
                }
            }
        }

        stage('Run Containers') {
            steps {
                script {
                    sh "docker-compose -p ${PROJECT_NAME} -f ${COMPOSE_FILE} up -d || exit 1"
                }
            }
        }

        stage('Post Build') {
            steps {
                echo "✅ Jenkins pipeline has completed running your containers."
                // Add testing scripts or curl health checks here if needed
            }
        }
    }

    post {
        always {
            echo "🧹 Cleaning up: stopping and removing containers"
            script {
                // Use || true to avoid failure if containers don't exist
                sh "docker-compose -p ${PROJECT_NAME} -f ${COMPOSE_FILE} down || true"
            }
        }
    }
}
