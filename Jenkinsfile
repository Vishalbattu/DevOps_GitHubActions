pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'test'
        DOCKER_IMAGE_TAG = 'latest'
        GIT_REPO_URL = 'https://github.com/Vishalbattu/DevOps.git'
    }

    stage('Install Docker') {
    steps {
        script {
            sh 'curl -fsSL https://get.docker.com -o get-docker.sh'
            sh 'sh get-docker.sh'
        }
    }
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
                }
            }
        }
    }
}
