pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'  // ID of Jenkins credential
        DOCKER_IMAGE = 'luckykilari/python-flask-app' 
        SONARQUBE_ENV = 'SonarQube'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LuckyKilari/Python_Sample_CICD.git' 
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=python-flask-app \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=http://13.232.225.234:9000 \
                          -Dsonar.login=$SONARQUBE_AUTH_TOKEN
                    '''
                }
            }
        }

        
        stage('Build Docker Image') {
            steps {
                script {                    
                    sh "docker build -t $DOCKER_IMAGE:${BUILD_NUMBER} ."                    
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
                sh "docker push $DOCKER_IMAGE:${BUILD_NUMBER}"
                
            }
        }
    }
    
}

