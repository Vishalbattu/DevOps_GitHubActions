pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'calculator'
        DOCKER_IMAGE_TAG = 'latest'
        GIT_REPO_URL = 'git@github.com:Vishalbattu/DevOps.git'
    }

    stages {
        stage('Clone and Build') {
            steps {
                script {
                    // Clone the Git repository
                    checkout([$class: 'GitSCM', 
                              branches: [[name: 'master']],
                              userRemoteConfigs: [[url: GIT_REPO_URL]]])

                    // Build Docker image
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", "-f .")
                }
            }
        }
    }
}
