pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image..."
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo "Deploying Docker Container..."
                // Purane container ko stop & remove kar do (agar chal raha ho)
                sh '''
                docker ps -q --filter "name=myapp-container" | grep -q . && docker stop myapp-container && docker rm myapp-container || true
                docker run -d -p 8081:8080 --name myapp-container myapp:latest
                '''
            }
        }
    }
}
