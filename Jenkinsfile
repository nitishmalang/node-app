pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure Node.js and npm are installed
                    sh 'node -v'
                    sh 'npm -v'
                    // Install npm dependencies
                    sh 'npm install'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Run tests
                    sh 'npm test'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    // Create a production build (if applicable)
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Trigger deployment (e.g., using AWS CodeDeploy)
                    sh 'aws deploy push --application-name your-app --s3-location s3://your-bucket/your-app.zip'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful.'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
