pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-demo"
        IMAGE_TAG = "latest"
        DOCKER_USERNAME = "Amrue320"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Installing Python dependencies...'
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

                bat 'copy app.py package\\app.py'

                bat 'copy requirements.txt package\\requirements.txt'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'

                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'

                bat 'docker tag %IMAGE_NAME%:%IMAGE_TAG% %DOCKER_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG%'
            }
        }

        stage('Docker Push') {
            steps {
                echo 'Logging into Docker Hub and pushing image...'

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'

                    bat 'docker push %DOCKER_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG%'

                    bat 'docker logout'
                }
            }
        }
    }

    post {

        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Jenkins pipeline completed successfully!'
        }

        failure {
            echo 'Jenkins pipeline failed. Please check the console output.'
        }
    }
}
