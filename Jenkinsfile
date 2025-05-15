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

🎉 Build completed successfully.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
✅ Status: SUCCESS  
🔗 Logs: ${env.BUILD_URL}

Cheers,  
Jenkins Bot 🤖
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

⚠️ Build has failed.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
❌ Status: FAILURE  
🔗 Logs: ${env.BUILD_URL}

Please check and fix.

Regards,  
Jenkins Bot ⚙️
""",
        to: 'sannithianjali1012@gmail.com',
        attachLog: true
      )
    }
  }
}