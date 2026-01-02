pipeline {
    agent any
    
    environment {
        // Enables the modern Docker builder for 2026
        DOCKER_BUILDKIT = '1'
        COMPOSE_DOCKER_CLI_BUILD = '1'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'ls -R'  // This will list all files in the console log
                // The dot (.) at the end is mandatory
                sh 'docker build -t flask-app:latest .'
            }
        }
        
        stage('Deploy with Docker Compose') {
            steps {
                // Stop existing containers if they are running
                sh 'docker compose down || true'
                // Start the application, rebuilding the flask image
                sh 'docker compose up -d --build'
            }
        }
    }
    
    post {
        failure {
            echo "Deployment failed. Check docker logs."
        }
    }
}
