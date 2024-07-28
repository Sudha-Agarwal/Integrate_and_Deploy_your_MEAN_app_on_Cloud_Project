pipeline {
    agent any
    
    stages{
        stage('Checkout'){
            steps{
                git url: 'https://github.com/Sudha-Agarwal/Integrate_and_Deploy_your_MEAN_app_on_Cloud_Project.git', branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t sudhaagarwal/health-app-backend:latest'
            }
        }
        stage('Test image') {
            steps {
                echo 'testing...'
                sh 'docker inspect --type=image sudhaagarwal/health-app-backend:latest'
            }
        }
        
        stage('Push'){
            steps{
        	     sh "sudo docker login -u sudhaagarwal -p"
                 sh "sudo docker tag health-app-backend sudhaagarwal/health-app-backend:latest"
                 sh 'sudo docker push sudhaagarwal/health-app-backend:latest'
            }
        }  
        stage('Deploy'){
            steps{
                echo 'deploying on another server'
                sh 'sudo docker stop health-app-backend || true'
                sh 'sudo docker rm health-app-backend || true'
                sh 'sudo docker run -d --name health-app-backend sudhaagarwal/health-app-backend:latest'
                
            }
        }
    }
}