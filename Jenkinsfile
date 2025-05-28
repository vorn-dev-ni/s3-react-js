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
        agent{
            docker {
                image 'amazon/aws-cli'
                args "--entrypoint=''"
                reuseNode true
            }
     
        }
        stage("Aws Configure") {
                sh """ 
                    aws --version
                 """
        }
    }
}