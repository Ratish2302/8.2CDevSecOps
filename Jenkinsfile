pipeline {
  agent any
  options { timestamps() }
  triggers {
    // Auto-build when new commits are pushed to GitHub (polls every 2 minutes)
    pollSCM('H/2 * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Ratish2302/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        // Install npm dependencies
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        // Run unit tests, continue even if they fail
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        // Generate coverage report
        sh 'npm run coverage || true'
      }
    }

    stage('Security Scan (npm audit)') {
      steps {
        // Run npm audit for vulnerabilities
        sh 'npm audit || true'
      }
    }
  }

  post {
    always {
      // Archive coverage report as artifact
      archiveArtifacts artifacts: 'coverage/**', allowEmptyArchive: true
    }
  }
}

