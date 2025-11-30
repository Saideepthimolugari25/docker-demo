pipeline { 
    agent any 
 
    environment { 
        DOCKERHUB_CREDENTIALS = credentials('molugarisaideepthi07') 
        IMAGE_NAME = "molugarisaideepthi07/flask-demo"
    } 
 
    stages { 
        stage('Checkout Code') { 
            steps { 
                echo "Checking out code..."
                checkout scm 
            } 
        } 
 
        stage('Build Docker Image') { 
            steps { 
                echo "Building Docker image..."
                bat "docker build -t %IMAGE_NAME%:latest ."
            } 
        } 
 
        stage('Login to Docker Hub') { 
            steps { 
                echo "Logging into Docker Hub..."
                bat "echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin"
            } 
        } 
 
        stage('Push Docker Image') { 
            steps { 
                echo "Pushing Docker image..."
                bat "docker push %IMAGE_NAME%:latest"
            } 
        } 
    } 
 
    post { 
        success { 
            echo "✔ Docker image successfully built and pushed to Docker Hub!" 
        } 
        failure { 
            echo "❌ Build failed. Check Jenkins logs." 
        } 
    } 
}

