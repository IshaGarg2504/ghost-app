pipeline {
    agent any
    stages {
        stage('Init') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Run docker compose"
                script {
                    docker-compose up
                }                

            }
        }

    }
}
