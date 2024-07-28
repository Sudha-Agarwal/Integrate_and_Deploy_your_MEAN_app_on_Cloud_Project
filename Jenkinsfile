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
                sh 'sudo docker build . -t sudhaagarwal/health-app-backend:latest'
            }
        }
        stage('Test image') {
            steps {
                echo 'testing...'
                sh 'sudo docker inspect --type=image sudhaagarwal/health-app-backend:latest'
            }
        }
        
        stage('Push'){
            steps{
        	     sh "sudo docker login -u sudhaagarwal -p Sudha@mangla1234"
                 sh "sudo docker tag health-app-backend sudhaagarwal/health-app-backend:latest"
                 sh 'sudo docker push sudhaagarwal/health-app-backend:latest'
            }
        }  
        stage('Deploy'){
            steps{
                echo 'deploying on another server'
                sh 'sudo docker stop nodetodoapp || true'
                sh 'sudo docker rm nodetodoapp || true'
                sh 'sudo docker run -d --name nodetodoapp basanagoudapatil/nodo-todo-app-test:latest'
                sh '''
                ssh -i Ubuntudemo.pem -o StrictHostKeyChecking=no ubuntu@44.211.144.201 <<EOF
                sudo docker login -u basanagoudapatil -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc
                sudo docker pull basanagoudapatil/nodo-todo-app-test:latest
                sudo docker stop nodetodoapp || true
                sudo docker rm nodetodoapp || true 
                sudo docker run -d --name nodetodoapp basanagoudapatil/nodo-todo-app-test:latest
                '''
            }
        }
    }
}