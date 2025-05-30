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
                    args '-u root --entrypoint=""'
                    reuseNode true
                }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 's3-aws', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh '''
                        aws --version
                        yum install jq -y
                        LATESTVERSION=$(aws ecs register-task-definition --cli-input-json file://task-definition.json | jq .taskDefinition.revision)
                        echo $LATESTVERSION
                        aws ecs update-service \
    --cluster learn-jenkin-prod \
    --service LearnJenkins-App-Prod-service-79ycmcel \
    --task-definition LearnJenkins-App-Prod:$LATESTVERSION 

   aws ecs wait services-stable \
    --cluster  learn-jenkin-prod \
    --services LearnJenkins-App-Prod-service-79ycmcel

                        
                 '''
                           cleanWs()
                }
            }
        }
    }
}
