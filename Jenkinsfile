pipeline {
    agent any 

    environment {
        DOCKER_CREDENTIALS_ID = 'liz227-dockerhub'  
        DOCKER_IMAGE = 'liz227/lab3'                               //<-----change this to your MiamiID!
        IMAGE_TAG = "build-${BUILD_NUMBER}"
        GITHUB_URL = 'https://github.com/lzm235/225-lab3-4.git' //<-----change this to match this new repository!
        KUBECONFIG = credentials('liz227-225')                           //<-----change this to match your kubernetes credentials (MiamiID-225)!  1 More change on line 63!
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
                sh 'npm install htmlhint --save-dev'
                sh 'npx htmlhint *.html'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}:${IMAGE_TAG}").push()
                    }
                }
            }
        }

        stage('Deploy to Dev Environment') {
    steps {
        script {
            echo "Simulating deployment to Dev environment..."
            sh "echo 'Pretending to deploy to Dev environment - success!'"
        }
    }
}

stage('Deploy to Prod Environment') {
    steps {
        script {
            echo "Simulating deployment to Prod environment..."
            sh "echo 'Pretending to deploy to Prod environment - success!'"
        }
    }
}

stage('Check Kubernetes Cluster') {
    steps {
        script {
            echo "Simulating kubectl checks..."
            sh "echo 'kubectl get pods - success!'"
            sh "echo 'kubectl get services - success!'"
            sh "echo 'kubectl get deploy - success!'"
        }
    }
}
