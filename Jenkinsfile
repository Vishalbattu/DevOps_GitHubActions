pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'test'
        DOCKER_IMAGE_TAG = 'latest'
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

                    // Run Docker-in-Docker with mounted Docker socket
                    //sh "docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v \$(pwd):/workspace -w /workspace docker:20.10 docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ."
                    sh "docker build -t calculator ."
                }
            }
        }
    }
}
