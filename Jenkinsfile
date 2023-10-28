node {
    // Define the Docker agent
    docker.image('node:18.17.1-buster-slim').withRun('-p 3000:3000') {
        // Inside the Docker container
        stage('Build') {
            // Steps for the 'Build' stage
            try {
                sh 'npm install'
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                throw e
            }
        }

        stage('Test') {
            // Steps for the 'Test' stage
            try {
                sh './jenkins/scripts/test.sh'
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                throw e
            }
        }
    }
}
