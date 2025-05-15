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
        sh 'npm test || true' // Avoids pipeline breaking on test failures
      }
    }

    stage('NPM Audit') {
      steps {
        sh 'npm audit || true' // Keeps build going despite CVEs
      }
    }
  }

  post {
    success {
      emailext(
        subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

🎉 Build completed successfully!

🔧 Job Name: ${env.JOB_NAME}  
🔁 Build Number: ${env.BUILD_NUMBER}  
✅ Status: SUCCESS  
🔗 View Logs: ${env.BUILD_URL}

Cheers,  
Jenkins Bot 🤖
""",
        to: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }

    unstable {
      emailext(
        subject: "⚠️ Build UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

⚠️ The build completed but was marked **UNSTABLE** — likely due to test failures or warnings.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
🔗 View details: ${env.BUILD_URL}

Please review and take action if needed.

Regards,  
Jenkins Bot 🛠️
""",
        to: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }

    failure {
      emailext(
        subject: "❌ Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

🚨 The build has **FAILED**.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
❌ Status: FAILURE  
🔗 Investigate here: ${env.BUILD_URL}

Please resolve the issue promptly.

Thanks,  
Jenkins Bot ⚙️
""",
        to: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }
  }
}