pipeline {
    agent any 
    
    environment {
        DOCKER_USER = credentials('DOCKER_USER')
        DOCKER_PASSWORD = credentials('DOCKER_PASSWORD') 
    }

    stages {
        stage('Build Image') {
            steps {
                sh "docker build -t node_app_image ." 
            }
        }
        
        stage('Run Container') {
            steps {
                sh "docker run -d --name node_app_container -p 3000:3000 node_app_image"
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh "docker login -u $DOCKER_USER -p $DOCKER_PASSWORD"
                sh "docker tag node_app_image:latest $DOCKER_USER/node_app_image:latest" 
                sh "docker push $DOCKER_USER/node_app_image:latest"
            }
        }
    }
}