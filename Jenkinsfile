pipeline {
    agent any
    
    environment {
    // Define environment variables if needed
    SSH_CREDENTIALS_ID = '3.83.67.227'
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
               sshagent([SSH_CREDENTIALS_ID]) {
                    // Running a simple command on the EC2 instance
                    bat """
                        ssh -o StrictHostKeyChecking=no ec2-user@%EC2_HOST% "echo 'Connected to EC2 instance!'"
                    """
                }
            }
        }
    }
}