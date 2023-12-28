pipeline {
    agent any

    stages {
        stage('Clone and Build') {
            steps {
                script {
                    // Clone the Git repository
                    git@github.com:Vishalbattu/DevOps.git

                    // Build Docker image
                    docker.build('vishalbattu/cicd:latest')
                }
            }
        }

        stage('Push to Docker Registry') {
            steps {
                script {
                    // Push Docker image to registry
                    docker.withRegistry('https://hub.docker.com/', 'docker') {
                        docker.image('vishalbattu/cicd:latest').push()
                    }
                }
            }
        }

        stage('Deploy on Server') {
            steps {
                script {
                    // SSH into the server and run Docker container
                    sshagent(['ssh-key']) {
                        sh 'ssh -o StrictHostKeyChecking=no ec2-user@13.40.223.103 "docker pull vishalbattu/cicd:latest && docker run -d -p 8080:5000 vishalbattu/cicd:latest"'
                    }
                }
            }
        }
    }
}
