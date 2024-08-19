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

        stage('Create K8s stuff ') {
            steps {
                //sh 'docker compose -f postgres-compose.yml up -d'

                dir('src/k8s/config'){
                     echo 'Running kubectl apply on config-map.yml'
                      sh 'sudo kubectl apply -f postgres-configmap.yml'
                }

                dir('src/k8s/storage'){
                    echo 'Creating pv and pvc for postgres db '
                     sh 'kubectl apply -f $(ls *.yml) '
                }

                dir('src/k8s/service'){
                     echo 'Creating service for postgres db '
                       sh 'kubectl apply -f postgres-service.yml'
                }

                dir('src/k8s/db'){
                echo 'Deploying postgres deployment '
                   sh 'kubectl apply -f postgres-service.yml '

                }
            }
        }
    }
}