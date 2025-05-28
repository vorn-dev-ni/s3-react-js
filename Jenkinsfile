pipeline {
    agent any

    environment {
        S3BUCKET = "jenkin-react-js"
    }

    stages {
        stage('Install and Build') {
            agent {
                docker {
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps {
                cleanWs()
                sh """
                    node --version
                    npm ci
                    npm run build
                """
            }
        }

        stage('AWS Deploy') {
            agent {
                docker {
                    image 'amazon/aws-cli:latest'
                    args '--entrypoint=""'
                    reuseNode true
                }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 's3-aws', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh """
                        aws --version
                        ls -la ./dist
                        aws s3 sync ./dist s3://${S3BUCKET} --delete
                        aws s3 ls s3://${S3BUCKET}
                    """
                }
            }
        }
    }
}
