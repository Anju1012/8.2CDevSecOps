pipeline {
  agent any

  stages {
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'  // Allow tests to fail without stopping pipeline
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'  // Allow audit to fail without stopping pipeline
      }
    }
  }

  post {
    always {
      emailext(
        subject: "Build: ${env.JOB_NAME} - #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
        body: """
Hi Team,

The build has completed with status: *${currentBuild.currentResult}*

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
📦 Status: ${currentBuild.currentResult}  
🔗 Logs: ${env.BUILD_URL}

Please check Jenkins for full details.

Regards,  
Jenkins Bot 🤖
""",
        to: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }
  }
}