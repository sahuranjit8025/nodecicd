
// Jenkinsfile
pipeline {
    agent any

    environment {
        // You can define environment variables here if needed
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
                sh 'npm install'
            }
        }

        stage('Build/Test') {
            steps {
                sh 'npm test' // Replace with 'npm run build' if you have a build script
            }
        }

        // Optional: Add a deployment stage if needed
        // stage('Deploy') {
        //     steps {
        //         sh './deploy.sh' // Or any deployment command/script
        //     }
        // }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
