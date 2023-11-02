node {
    docker.image("node:18.17.1-buster-slim").inside("-u root -p 3000:3000") {
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

        stage('Deploy') {
            try {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            } catch (Exception e) {
                currentBuild.result = 'FAILURE'
                throw e
            }
        }
    }
}

