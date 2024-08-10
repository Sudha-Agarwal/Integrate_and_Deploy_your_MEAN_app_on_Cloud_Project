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
        	     bat "sudo docker login -u sudhaagarwal -p Sudha@123"
                 bat "sudo docker tag health-app-backend sudhaagarwal/health-app-backend:latest"
                 bat 'sudo docker push sudhaagarwal/health-app-backend:latest'
            }   
        }
    }
}