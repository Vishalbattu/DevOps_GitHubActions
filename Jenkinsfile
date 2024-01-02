pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'webcalculator'
        DOCKER_IMAGE_TAG = 'latest'
        DOCKER_HUB_REGISTRY = 'https://registry.hub.docker.com/'
        DOCKER_HUB_CREDENTIALS_ID = 'vishal'
        GIT_REPO_URL = 'https://github.com/Vishalbattu/DevOps.git'
    }

    stages {
        stage('Clone and Build') {
            steps {
                script {
                    // Print the current working directory
                    sh "pwd"

                    // Clone the public GitHub repository
                    checkout([$class: 'GitSCM', 
                              branches: [[name: 'master']],
                              userRemoteConfigs: [[url: GIT_REPO_URL]]])

                    // List the contents of the current directory
                    sh "ls -la"

                    // Print the Docker version for debugging
                    sh "docker --version"

                    // Use the Docker client configured through Docker Socket Binding
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", ".")

                    // Push Docker image to Docker Hub
                    docker.withRegistry(DOCKER_HUB_REGISTRY, --username 'vishalbattu' --password 'Vishalbhattu@8') {
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
