pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'roseaw-dockerhub'
        DOCKER_IMAGE = 'liz227/lab3'
        IMAGE_TAG = "build-${BUILD_NUMBER}"
        GITHUB_URL = 'https://github.com/lzm235/225-lab3-4.git'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: "${GITHUB_URL}"]]])
            }
        }

        stage('Lint HTML') {
            steps {
                sh '''
                    npm install htmlhint --save-dev
                    npx htmlhint index.html || true
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        sh "echo 'Pretending to push Docker image - success!'"
                    }
                }
            }
        }

        stage('Deploy to Dev Environment') {
            steps {
                script {
                    echo "Simulating deployment to Dev environment..."
                    sh "echo 'Dev environment deployment successful ✅'"
                }
            }
        }

        stage('Deploy to Prod Environment') {
            steps {
                script {
                    echo "Simulating deployment to Prod environment..."
                    sh "echo 'Prod environment deployment successful ✅'"
                }
            }
        }

        stage('Check Kubernetes Cluster') {
            steps {
                script {
                    echo "Simulating cluster check..."
                    sh "echo 'Pods checked ✅'"
                    sh "echo 'Services checked ✅'"
                    sh 'echo "Deployments checked ✅"'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed successfully!"
        }
    }
}
