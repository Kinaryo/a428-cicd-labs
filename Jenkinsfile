pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval'){
            steps{input message: 'lanjutkan ke tahapan Deploy ? (Klik "Proceed" untuk mengakhiri)' 
        }}
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                sleep time: 60, unit: 'SECONDS'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}