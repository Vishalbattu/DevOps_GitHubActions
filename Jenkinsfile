pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'vishalbattu/webcalculator'
        DOCKER_IMAGE_TAG = 'latest'
        DOCKER_HUB_REGISTRY = 'https://registry.hub.docker.com/'
        DOCKER_HUB_CREDENTIALS_ID = 'vishal'
        GIT_REPO_URL = 'https://github.com/Vishalbattu/DevOps.git'
        DOCKER_NODE_NAME = 'mynode' // Name of the Jenkins node where you want to deploy
    }

    stages {
        stage('Clone and Build') {
            steps {
                script {
                    // ... existing steps ...

                    // Use the Docker client configured through Docker Socket Binding
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", ".")

                    // Push Docker image to Docker Hub
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS_ID) {
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }

        stage('Deploy on Server') {
            steps {
                script {
                    // Deploy the Docker image on the specified node
                    node(DOCKER_NODE_NAME) {
                        // Use credentials to pull Docker image
                        withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS_ID, usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                            // Pull the Docker image on the node
                            docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").pull()

                            // Run the Docker image on the node
                            docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")
                                .run("-d -p 8081:5000 vishalbattu/cicd:latest")
                        }
                    }
                }
            }
        }
    }
}
