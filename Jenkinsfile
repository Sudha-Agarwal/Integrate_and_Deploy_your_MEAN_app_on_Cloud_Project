pipeline {
    agent any
    
    environment {
    // Define environment variables if needed
    SSH_CREDENTIALS_ID = 'my-ssh-id'
    EC2_HOST = '3.83.67.227'
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


        stage('Deploy'){
            steps
            {
                ssh -i C:\\Users\\Lenovo\\Downloads\\key1.pem ec2-user@3.83.67.227
            }
        }
    }
}