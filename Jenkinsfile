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
                    sh "docker-compose -p ${PROJECT_NAME} -f ${COMPOSE_FILE} build"
                }
            }
        }

        stage('Run Containers') {
            steps {
                script {
                    sh "docker-compose -p ${PROJECT_NAME} -f ${COMPOSE_FILE} up -d"
                }
            }
        }

        stage('Post Build') {
            steps {
                echo "Jenkins pipeline has completed running your containers."
                // Add any testing or health check scripts here if required
            }
        }
    }

    post {
        always {
            echo "Cleaning up: stopping and removing containers"
            sh "docker-compose -p ${PROJECT_NAME} -f ${COMPOSE_FILE} down"
        }
    }
}
