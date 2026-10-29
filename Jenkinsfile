pipeline{
    agent any 
    environment{
        DOCKERHUB_USERNAME = "yacks"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}/nodejs-cicd-app2"
        APP_PORT = "3000"
        CONTAINER_NAME = "nodejs-apps"
    }
    stages{
        stage("Checkout source code"){
            steps{
                checkout scm
            }
        }

        stage("Install dependencies"){
            steps{
                sh "npm ci"
            }
        }

         stage("Build docker image"){
            steps{
                sh """
                docker build \
                -t ${IMAGE_NAME}:${BUILD_NUMBER} \
                -t ${IMAGE_NAME}:latest .
                """
            }
        }
        stage("Push to docker hub"){
            steps{
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKERHUB_USERNAME',
                        passwordVariable: 'DOCKER_TOKEN'
                    )
                ]){
                    sh """
                    echo "$DOCKER_TOKEN" | docker login -u "$DOCKERHUB_USERNAME" --password-stdin
                    docker push ${IMAGE_NAME}:${BUILD_NUMBER}
                    docker push ${IMAGE_NAME}:latest
                    docker logout
                    """
                }
            }
        }
    }
}
