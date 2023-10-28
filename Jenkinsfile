node {
    docker.image("node:18.17.1-buster-slim").inside("-u root -p 3000:3000") {
        stage('Build') {
            try {
                checkout scm
                sh 'apt-get update'
                sh 'apt-get install -y nodejs'
                sh 'apt-get install -y npm'
                sh 'npm install'
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                throw e
            }
        }

        stage('Test') {
            try {
                sh './jenkins/scripts/test.sh'
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                throw e
            }
        }
    }
}

