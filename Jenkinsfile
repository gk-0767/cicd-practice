
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Getting application code from GitHub'
                checkout scm
            }
        }

        stage('Setup Python') {
            steps {
                sh '''
                    python3 --version
                    python3 -m venv .venv
                    .venv/bin/pip install --upgrade pip
                    .venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '.venv/bin/python -m pytest -v'
            }
        }
               stage('Build Docker Image') {
            steps {
                sh 'sudo docker build -t employee-service:1.0 .'
            }
        }
    }
    post {
        success {
            echo 'CI pipeline completed successfully!'
        }
        failure {
            echo 'CI pipeline failed. Check the Console Output.'
        }
    }
}
