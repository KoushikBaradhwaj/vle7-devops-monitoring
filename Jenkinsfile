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
                sh 'docker build -t vle7-monitoring:v1 .'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker image inspect vle7-monitoring:v1'
                echo 'Docker image build and inspection successful'
            }
        }

        stage('Export Image') {
            steps {
                sh 'docker save vle7-monitoring:v1 -o vle7-monitoring-v1.tar'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    sudo k3s ctr images import vle7-monitoring-v1.tar
                    KUBECONFIG=/var/lib/jenkins/k3s.yaml kubectl set image deployment/vle7-app nginx=docker.io/library/vle7-monitoring:v1
                    KUBECONFIG=/var/lib/jenkins/k3s.yaml kubectl rollout status deployment/vle7-app
                '''
            }
        }
    }
}
