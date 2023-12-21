pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('your-aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('your-aws-secret-access-key')
        S3_BUCKET_NAME = 'react-to-do-app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        // stage('Stop Existing Server') {
        //     steps {
        //         script {
        //             sh 'cd /opt/checkout/react-todo-app/'
        //             sh 'npm stop'  
        //         }
        //     }
        // }

        // stage('Pull Fresh Code') {
        //     steps {
        //         script {
        //             sh 'cd /opt/checkout/react-todo-app/'
        //             git pull origin master  // Use your Git repository and branch
        //         }
        //     }
        // }

        stage('Start NPM') {
            steps {
                script {
                    sh 'cd /opt/checkout/react-todo-app/'
                    sh 'npm install'
                    sh 'npm start'  
                }
            }
        }

        stage('Build and Push to S3') {
            steps {
                script {
                    sh 'cd /opt/checkout/react-todo-app/'
                    // Upload build files to S3
                    sh 'aws s3 sync build/ s3://$S3_BUCKET_NAME/'
                }
            }
        }
    }
}
