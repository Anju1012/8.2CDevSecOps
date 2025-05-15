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
    always {
      emailext(
        subject: "📦 Build Result: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """
Hi Team,

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
📊 Status: ${currentBuild.currentResult}  
🔗 Logs: ${env.BUILD_URL}

Best,  
Jenkins Bot 🤖
""",
        to: 'd0fd824e61-acd2b8@inbox.mailtrap.io', // OR your Gmail if configured globally
        attachLog: true
      )
    }
  }
}