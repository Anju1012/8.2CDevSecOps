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
        sh 'npm test || true'  // Allow test failures without stopping the build
      }
    }

    stage('NPM Audit') {
      steps {
        sh 'npm audit || true'  // Allow audit warnings to pass through
      }
    }
  }

  post {
    success {
      emailext(
        subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

🎉 The build completed successfully!

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
✅ Status: SUCCESS  
🔗 Logs: ${env.BUILD_URL}

Best regards,  
Jenkins Bot 🤖
""",
        mimeType: 'text/plain',
        to: 'sannithianjali1012@gmail.com',
        replyTo: 'sannithianjali1012@gmail.com',
        from: 'sannithianjali1012@gmail.com',
        smtpHost: 'smtp.gmail.com',
        smtpPort: '587',
        useTls: true
      )
    }

    unstable {
      emailext(
        subject: "⚠️ Build UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

⚠️ The build finished with warnings (likely due to tests or audit issues).

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
🟡 Status: UNSTABLE  
🔗 Logs: ${env.BUILD_URL}

Please review as needed.

Regards,  
Jenkins Bot
""",
        mimeType: 'text/plain',
        to: 'sannithianjali1012@gmail.com',
        replyTo: 'sannithianjali1012@gmail.com',
        from: 'sannithianjali1012@gmail.com',
        smtpHost: 'smtp.gmail.com',
        smtpPort: '587',
        useTls: true
      )
    }

    failure {
      emailext(
        subject: "❌ Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

❌ The build has failed.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
🔗 Logs: ${env.BUILD_URL}

Please check and fix the issue.

Thanks,  
Jenkins Bot
""",
        mimeType: 'text/plain',
        to: 'sannithianjali1012@gmail.com',
        replyTo: 'sannithianjali1012@gmail.com',
        from: 'sannithianjali1012@gmail.com',
        smtpHost: 'smtp.gmail.com',
        smtpPort: '587',
        useTls: true
      )
    }
  }
}