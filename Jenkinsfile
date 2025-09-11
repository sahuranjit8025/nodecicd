pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
        AWS_REGION = 'ap-south-1'
        ECR_REPO = 'sample-node-app'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/sahuranjit8025/nodecicd.git', 
                    credentialsId: 'a6cd476b-d7d0-4304-a75a-d93bd962bd7a'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Get AWS Account ID') {
            steps {
                script {
                    env.ACCOUNT_ID = sh(script: "aws sts get-caller-identity --query Account --output text", returnStdout: true).trim()
                    env.ECR_URL = "${env.ACCOUNT_ID}.dkr.ecr.${env.AWS_REGION}.amazonaws.com/${env.ECR_REPO}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${ECR_REPO}:${IMAGE_TAG} ."
            }
        }

        stage('Login to ECR') {
            steps {
                sh """
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin $ECR_URL
                """
            }
        }

        stage('Tag & Push Image') {
            steps {
                sh """
                docker tag ${ECR_REPO}:${IMAGE_TAG} ${ECR_URL}:${IMAGE_TAG}
                docker push ${ECR_URL}:${IMAGE_TAG}
                """
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
        }
        failure {
            echo '❌ Build failed. Please check the logs.'
        }
    }
}
