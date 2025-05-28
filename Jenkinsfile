pipeline {

    agent any
    environment {
        S3BUCKET="jenkin-react-js"
    }
    stages {
            // stage('Cleaning WorkSpace') {

            //     steps {

            //         cleanWs()
           
            //     }
            // }
     stage("Aws Configure") {
         agent{
            docker {
                image 'amazon/aws-cli:latest'
                args "--entrypoint=''"
                reuseNode true
            }
     
        }
             steps {
                withCredentials([usernamePassword(credentialsId: 's3-aws', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                   sh """ 


                    aws --version
                    aws s3 sync ./dist s3://${S3BUCKET} --delete
                    aws s3 ls
                 """
}
             }
        }

    }

}