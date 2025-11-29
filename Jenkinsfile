pipeline { 
    agent any 
 
    environment { 
        DOCKERHUB_CREDENTIALS = credentials('molugarisaideepthi07') 
        IMAGE_NAME = "molugarisaideepthi07/docker-demo" 
    } 
 
    stages { 
        stage('Checkout Code') { 
            steps { 
                echo "Checking out repository..."
                git url: 'https://github.com/Saideepthimolugari25/docker-demo.git', branch: 'main'
            } 
        } 
 
        stage('Build Docker Image') { 
            steps { 
                echo "Building Docker Image..."
                bat "docker build -t %IMAGE_NAME% ."
            } 
        } 
 
        stage('Login to Docker Hub') { 
            steps { 
                echo "Logging into Docker Hub..."
                bat """
                echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                """
            } 
        } 
 
        stage('Push to Docker Hub') { 
            steps { 
                echo "Pushing image to Docker Hub..."
                bat "docker push %IMAGE_NAME%"
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
