pipeline {
    agent { docker { image 'node:latest'' } }
    environment {
        HOME = '.'
    }
    // environment {
    //     CI = 'true'
    // }
    stages {
        stage('Build') {
            steps {
                sh 'npm cache clean --force'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'dev-1234'
            }
            steps {
                sh 'scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'scripts/kill.sh'
            }
        }
        stage('Deploy for fix') {
            when {
                branch 'fix-1234'
            }
            steps {
                sh 'scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'scripts/kill.sh'
            }
        }
    }
}
