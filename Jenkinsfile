pipeline {
    agent any

    environment {
        S3BUCKET = "jenkin-react-js"
        AWS_DEFAULT_REGION="us-east-1"
    }

    stages {
    

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
                        aws ecs register-task-definition --cli-input-json file://task-definition.json
                        aws ecs update-service \
    --cluster learn-jenkin-prod \
    --service LearnJenkins-App-Prod-service-79ycmcel \
    --task-definition LearnJenkins-App-Prod:2

                        
                    """
                           cleanWs()
                }
            }
        }
    }
}
