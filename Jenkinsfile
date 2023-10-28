node {
    try {
        stage('Checkout SCM') {
            checkout scm
        }
        
        stage('Build') {
            def dockerImage = 'node:18.17.1-buster-slim'
            def container = docker.image(dockerImage).withRun('-p 3000:3000') {
                sh 'npm install'
            }
        }
        
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
