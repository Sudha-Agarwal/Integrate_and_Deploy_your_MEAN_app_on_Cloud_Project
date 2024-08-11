pipeline{
    agent any

    stages{
        stage('checkout'){
            steps{
                git url: 'file:///g:/Sudha/Simplilearn/code/Health-app', branch: 'main'
            }
        }

        stage('Build'){
            steps{
                bat 'docker-compose build'
            }
        }
        stage('Tag Image'){
            steps{
                bat 'docker tag health-app sudhaagarwal/health-app:latest'
            }
        }
    }
}