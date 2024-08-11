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
    }
}