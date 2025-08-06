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
                sh '''
                    # Purana container agar exist karta hai to force stop & remove
                    docker ps -a -q --filter "name=myapp-container" | grep -q . && docker rm -f myapp-container || true
                    
                    # Naya container run karo on port 8081
                    docker run -d -p 8081:8080 --name myapp-container myapp:latest
                '''
            }
        }
    }
}
