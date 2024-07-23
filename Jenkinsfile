pipeline {
    agent any

    environment {
        GITHUB_REPOSITORY = 'https://github.com/tapiwanasheMbizvo/database-infra.git'

    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: "${GITHUB_REPOSITORY}", branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'docker compose -f postgres-compose.yml up'
            }
        }
    }
}