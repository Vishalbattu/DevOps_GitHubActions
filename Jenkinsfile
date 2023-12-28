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
                    // Clone the public GitHub repository
                    checkout([$class: 'GitSCM', 
                              branches: [[name: 'master']],
                              userRemoteConfigs: [[url: GIT_REPO_URL]]])

                    // Build Docker image
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", ".")
                }
            }
        }
    }
}
