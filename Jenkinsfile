pipeline{
    agent any
    environment{
        SSH_KEY_PATH='C:\\Users\\Lenovo\\Downloads\\login2.pem'
        SSH_USER='ec2-user'
        SSH_HOST='44.211.154.250'
    }

    stages{
        stage('checkout'){
            steps{
                git url: 'file:///g:/Sudha/Simplilearn/code/Health-app', branch: 'main'
            }
        }

        stage('Build'){
            steps{
                bat 'docker-compose build --no-cache'
            }
        }
        stage('Tag Image'){
            steps{
                bat 'docker tag health-app sudhaagarwal/health-app:latest'
            }
        }
        stage('Push Image'){
            steps{
                bat 'docker login -u sudhaagarwal -p Sudha@123'
                bat 'docker push sudhaagarwal/health-app:latest'
            }
        }
        stage('Deploy'){
            steps{
                bat """
                ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${SSH_USER}@${SSH_HOST} ^
                "docker stop health-app || true && docker rm health-app || true && docker rmi sudhaagarwal/health-app:latest && docker pull sudhaagarwal/health-app:latest && docker run -d --name health-app -p 3000:3000 sudhaagarwal/health-app:latest
                """
            }
        }
    }
}