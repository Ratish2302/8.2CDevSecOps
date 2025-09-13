pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git branch: 'main',
                    url: 'https://github.com/Ratish2302/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'npm audit || true'
            }
        }
    }

    post {
        success {
            mail to: 'sharmaratish02@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """
Good news!

Your Jenkins pipeline job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} was SUCCESSFUL.

You can view the full build details here:
${env.BUILD_URL}
                 """
        }

        failure {
            mail to: 'sharmaratish02@gmail.com',
                 subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """
Attention!

Your Jenkins pipeline job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} has FAILED.

Check the console output here for details:
${env.BUILD_URL}console
                 """
        }
    }
}
