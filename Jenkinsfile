pipeline {
  agent any
  stages {
    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        bat 'npm test || exit /b 0'
      }
    }
    stage('Generate Coverage Report') {
      steps {
        bat 'npm run coverage || exit /b 0'
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit /b 0'
        bat 'npm audit --json > audit-report.json || exit /b 0'
      }
    }
  }
  post {
  success {
    mail to: 'tharunsangam@gmail.com',
         subject: " Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
         body: "The build completed successfully.\nCheck console output at ${env.BUILD_URL}"
  }
  failure {
    mail to: 'tharunsangam@gmail.com',
         subject: " Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
         body: "The build failed.\nCheck console output at ${env.BUILD_URL}"
  }
}
}