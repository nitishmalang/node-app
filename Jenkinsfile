pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-west-2'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/your-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                withAWS(credentials: 'aws-credentials-id', region: 'us-west-2') {
                    sh 'aws deploy push --application-name your-app --s3-location s3://your-bucket/your-app.zip'
                    sh 'aws deploy create-deployment --application-name your-app --s3-location bucket=your-bucket,key=your-app.zip,bundleType=zip --deployment-group-name your-deployment-group'
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deploy successful'
        }
        failure {
            echo 'Build or deploy failed'
        }
    }
}
