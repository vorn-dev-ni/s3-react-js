pipeline {

    agent any
    stages {
            stage('Cleaning WorkSpace') {

                steps {

                    cleanWs()
           
                }
            }

    }

    stages {
      
        stage("Aws Configure") {
         agent{
            docker {
                image 'amazon/aws-cli'
                args "--entrypoint=''"
                reuseNode true
            }
     
        }
             steps {
                   sh """ 
                    aws --version
                 """
             }
        }
    }
}