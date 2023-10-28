node {
    docker.image('node:18.17.1-buster-slim').withRun('-p 3000:3000') { c ->
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    }
}
