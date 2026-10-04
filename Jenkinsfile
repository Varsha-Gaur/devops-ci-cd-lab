pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv .venv
                    ./.venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    ./.venv/bin/python -m pytest
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    rm -rf build
                    mkdir -p build
                    cp -r app build/
                    cp requirements.txt build/
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    rm -rf deployed
                    mkdir -p deployed
                    cp -r build/* deployed/
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully.'
        }

        failure {
            echo 'CI/CD pipeline failed.'
        }
    }
}