pipeline {
agent any

  stages {
        stage('Clone ') {
            steps {
              checkout scmGit(branches: [[name: '*/Devops']], extensions: [], userRemoteConfigs: [[credentialsId: 'GIT', url: 'https://github.com/Vishalbattu/DevOps.git']])
            }
        }
  }  
  
  
}
