pipeline { 
    agent any 
 
    environment { 
        DOCKERHUB_CREDENTIALS = credentials('molugarisaideepthi07') 
        IMAGE_NAME = "molugarisaideepthi07/docker-demo" 
    } 
 
    stages { 
        stage('Checkout Code') { 
            steps { 
                checkout scm 
            } 
        } 
 
        stage('Build Docker Image') { 
            steps { 
                bat "docker build -t %IMAGE_NAME% ." 
            } 
        } 
 
        stage('Login to Docker Hub') { 
            steps { 
                bat "powershell -Command \"echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin\"" 
            } 
        } 
 
        stage('Push to Docker Hub') { 
            steps { 
                bat "docker push %IMAGE_NAME%" 
            } 
        } 
    } 
 
    post { 
        success { 
            echo "     Docker image successfully built and pushed to Docker Hub!" 
        } 
        failure { 
            echo "    Build failed. Check Jenkins logs." 
        } 
    } 
}