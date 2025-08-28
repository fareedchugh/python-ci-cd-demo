pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR-USERNAME/python-ci-cd-demo.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'pip install -r requirements.txt'
                sh 'pytest --cov=app --cov-report=xml --junitxml=tests/test-results.xml'
            }
            post {
                always {
                    junit 'tests/test-results.xml'
                    publishCoverage adapters: [coberturaAdapter('coverage.xml')]
                }
            }
        }

        stage('Security Scan') {
            steps {
                sh 'bandit -r app/'
                sh 'safety check -r requirements.txt'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop myapp || true && docker rm myapp || true'
                sh 'docker run -d -p 5000:5000 --name myapp myapp:latest'
            }
        }
    }
}
