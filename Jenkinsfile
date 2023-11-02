node {
    docker.image("node:16-buster-slim").inside("-u root -p 3000:3000") {
        stage('Build') {
            try {
                checkout scm
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

        stage('Manual Approval') {
                    try {
                        checkout scm
                        input message: 'Lanjutkan ke tahap Deploy?'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }

        stage('Deploy') {
            try {
                sh './jenkins/scripts/deliver.sh'
                sleep time: 60, unit: 'SECONDS'
                sh './jenkins/scripts/kill.sh'
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                throw e
            }
        }
    }
}

