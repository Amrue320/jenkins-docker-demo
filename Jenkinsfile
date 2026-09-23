pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-demo"
        IMAGE_TAG = "latest"
        DOCKER_REGISTRY = "docker.io"
        // Set DOCKER_USERNAME as a Jenkins credential/environment value.
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Installing dependencies and preparing the application...'
                bat 'python -m pip install --upgrade pip'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests...'
                bat 'python -m pytest -v'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating application package...'
                bat 'if not exist package mkdir package'
                bat 'copy app.py package\app.py'
                bat 'copy requirements.txt package\requirements.txt'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Docker Push') {
            steps {
                echo 'Push stage is ready for Docker Hub credentials.'
                echo 'Configure a Jenkins credential and Docker Hub username before enabling the push command.'
                // Example after configuring credentials:
                // withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                //     bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                //     bat 'docker tag %IMAGE_NAME%:%IMAGE_TAG% %DOCKER_USER%/%IMAGE_NAME%:%IMAGE_TAG%'
                //     bat 'docker push %DOCKER_USER%/%IMAGE_NAME%:%IMAGE_TAG%'
                // }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Jenkins pipeline completed successfully.'
        }
        failure {
            echo 'Jenkins pipeline failed. Check the stage logs.'
        }
    }
}
