pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'vishalbattu/webcalculator'
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
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                    docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }

                }
            }
        }
    
    
    stage('Deploy on Server') {
            steps {
                script {
                    // SSH into the server and run Docker container
                    sshagent(['ssh-key']) {
                        sh 'ssh -o StrictHostKeyChecking=no ec2-user@13.40.223.103 "docker pull vishalbattu/webcalculator:latest && docker run -d -p 8080:5000 vishalbattu/cicd:latest"'
                    }
                }
            }
        }}
}
