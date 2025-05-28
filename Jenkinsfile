pipeline {

    agent any
    stages {
            stage('Cleaning WorkSpace') {

                steps {

                    cleanWs()
           
                }
            }
     stage("Aws Configure") {
         agent{
            docker {
                image 'amazon/aws-cli:latest'
                args "--entrypoint=''"
                reuseNode true
            }
     
        }
             steps {
                   sh """ 
                    aws --version
                    aws ls
                 """
             }
        }

    }

}