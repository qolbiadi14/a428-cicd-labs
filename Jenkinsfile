pipeline {
    agent {
        docker {
            image 'node:18.17.1-buster-slimgit' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
    }
}
