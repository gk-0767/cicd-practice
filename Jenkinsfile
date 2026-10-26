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
                sh 'docker build -t employee-service:1.0 .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f employee-app || true
                    docker run -d --name employee-app -p 5000:5000 employee-service:1.0
                    sleep 3
                    curl --fail http://localhost:5000/health
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD pipeline failed. Check the Console Output.'
        }
    }
}

        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD pipeline failed. Check the Console Output.'
        }
    }
}
