pipeline {
    agent any

    environment {
        SSH_CREDENTIALS_ID = 'my-ssh-id'
        SSH_KEY_PATH = 'C:\\Users\\Lenovo\\Downloads\\login.pem'
        SSH_USER = 'ec2-user'
        SSH_HOST = '3.88.226.4'
    }

    stages{
        stage('Checkout'){
            steps{
                git url: 'file:///g:/Sudha/Simplilearn/code/Health-app', branch: 'main'
            }
        }
        stage('Build '){
            steps{
                bat 'docker compose '
            }
        }
        stage("Tag Image"){
            steps{
                bat 'docker tag mean-app-backend sudhaagarwal/mean-app-backend:latest'
            }
        }

        stage('Push Image'){
            steps{
        	     bat "docker login -u sudhaagarwal -p Sudha@123"
                 bat "docker tag health-app-backend sudhaagarwal/health-app-backend:latest"
                 bat 'docker push sudhaagarwal/health-app-backend:latest'
            }   
        }

    stages{

        stage('Test'){
            steps{
                bat 'whoami'
            }
        }

        stage('Deploy'){
            steps
            {
                // Use double backslashes for Windows paths or forward slashes
                bat """
                    ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${SSH_USER}@${SSH_HOST} ^
                    "docker stop health-app-backend || true && docker rm health-app-backend || true && docker login -u sudhaagarwal -p Sudha@123 && docker run -d --name health-app-backend -p 3000:3000 sudhaagarwal/health-app-backend:latest "
                """
            }
        }
    }
}