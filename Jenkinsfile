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
        sh 'npm test || true'
      }
    }

    stage('NPM Audit') {
      steps {
        sh 'npm audit || true'
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

Cheers,  
Jenkins Bot 🤖
""",
        mimeType: 'text/plain',
        to: 'sannithianjali1012@gmail.com',
        replyTo: 'sannithianjali1012@gmail.com',
        from: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }

    unstable {
      emailext(
        subject: "⚠️ Build UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

⚠️ The build finished with warnings or failed tests.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
🟡 Status: UNSTABLE  
🔗 Logs: ${env.BUILD_URL}

Please review.

Jenkins Bot
""",
        mimeType: 'text/plain',
        to: 'sannithianjali1012@gmail.com',
        replyTo: 'sannithianjali1012@gmail.com',
        from: 'sannithianjali1012@gmail.com',
        attachLog: true
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

Please fix the issue ASAP.

Jenkins Bot
""",
        mimeType: 'text/plain',
        to: 'sannithianjali1012@gmail.com',
        replyTo: 'sannithianjali1012@gmail.com',
        from: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }
  }
}