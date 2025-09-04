        // Jenkinsfile
        pipeline {
            agent any

            stages {
                stage('Checkout') {
                    steps {
                        git url: 'https://github.com/sahuranjit8025/nodecicd.git', credentialsId: 'a6cd476b-d7d0-4304-a75a-d93bd962bd7a' // Replace with actual URL and ID
                    }
                }
                stage('Install Dependencies') {
                    steps {
                        sh 'npm install'
                    }
                }
                stage('Build/Test') {
                    steps {
                        sh 'npm test' // Or 'npm run build' if you have a build step
                    }
                }
                // Add more stages for deployment, etc., as needed
            }
        }