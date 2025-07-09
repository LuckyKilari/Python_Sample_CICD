pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'  // ID of Jenkins credential
        DOCKER_IMAGE = 'luckykilari/python-flask-app' 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LuckyKilari/Python_Sample_CICD.git' 
            }
        }

        
        stage('Build Docker Image') {
            steps {
                script {
                    // sh "docker build -t $DOCKER_IMAGE:latest ."
                    // def version = "${BUILD_NUMBER}"
                    // sh "docker build -t $DOCKER_IMAGE:$version ."
                    sh "docker build -t $DOCKER_IMAGE:${BUILD_NUMBER} ."
                    // Optionally also tag 'latest'
                    // sh "docker tag $DOCKER_IMAGE:$version $DOCKER_IMAGE:latest"
                }
            }
        }

        stage('DockerHub Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    """
                }
            }
        }       

        stage('Push Image') {
            steps {
                // def version = "${BUILD_NUMBER}"
                // sh "docker push $DOCKER_IMAGE:$version"
                sh "docker push $DOCKER_IMAGE:${BUILD_NUMBER}"
                // sh "docker push $DOCKER_IMAGE:latest"
            }
        }
    }
    
}

