pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t vle7-monitoring:latest .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker image inspect vle7-monitoring:latest'
                echo 'Docker image build and inspection successful'
            }
        }
    }
}
