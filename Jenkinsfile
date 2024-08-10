pipeline {
    agent any
    
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
                def remote = [:]
                remote.name = 'ec2'
                remote.host = 'your-ec2-public-ip'
                remote.user = 'ec2-user' // Using 'ec2-user' for Amazon Linux
                remote.identityFile = '/path/to/your/private-key.pem'
                remote.identityFile = 'C:\\Users\\Lenovo\\Downloads\\key1.pem' // Windows path format

            }
        }
    }
}