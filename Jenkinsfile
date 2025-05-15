pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Anju1012/8.2CDevSecOps.git'
      }
    }

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

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }
  }
}post {
  success {
    emailext(
      subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
      body: """
Hi Team,

🎉 Great news! Your Jenkins build completed **successfully**.

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

⚠️ The Jenkins build has **FAILED**.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
❌ Status: FAILURE  
🔗 View details: ${env.BUILD_URL}

Please investigate and fix the issue.

Thanks,  
Jenkins Bot ⚙️
""",
      to: 'sannithianjali1012@gmail.com',
      attachLog: true
    )
  }

  always {
    echo 'Email notification logic completed.'
  }
}