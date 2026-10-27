pipeline{
    agent any
    environment{
        DOCKER_IMAGE = 'yacks/cicd-node-api2'
        DOCKER_CREDS = 'dockerhub-credential'
        EC2_USER = 'ubuntu'
        // EC2_HOST = 'EC2_PUBLIC_IP_OR_DNS'
        CONTAINER_NAME = 'cicd-node-api2'
        APP_PORT = '3000'
        // EC2_SSH_CREDS = 'ec2-ssh-key'
    }

    stages {
        stage("Check out jobs"){
            steps{
                checkout scm
            }

        }

        stage("Install dependencies"){
            steps{
                sh 'npm ci'
            }
            
        }

        stage("Test Code"){
            steps{
                sh 'npm test'
            }
            
        }
    }
}