
// Jenkinsfile
pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
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
                bat 'npm install'
            }
        }

        /* stage('Build/Test') {
            steps {
                bat 'npm test' // Or 'npm run build' if you have a build step
            }
        } */
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
