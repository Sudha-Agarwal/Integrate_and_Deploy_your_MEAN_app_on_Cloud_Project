pipeline {
    agent any
    
    stages{
        stage('Checkout'){
            steps{
                git url: 'file:///g:/Sudha/Simplilearn/code/Health-app', branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t health-app-backend:latest'
            }
        }
        
    }
}