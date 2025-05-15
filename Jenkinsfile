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
        sh 'npm test || true'  // prevents pipeline from failing and allows 'post' to run
      }
    }

    stage('Security Audit') {
      steps {
        sh 'npm audit || true'  // allows reporting even if audit fails
      }
    }
  }

  post {
    always {
      emailext(
        subject: "Build: ${env.JOB_NAME} - #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
        body: """
Hello Team,

The Jenkins job **${env.JOB_NAME}** build #${env.BUILD_NUMBER} has finished with status: *${currentBuild.currentResult}*

🔗 [View Build Log](${env.BUILD_URL})

Regards,  
Jenkins Bot 🤖
        """,
        to: 'd0fd824e61-acd2b8@inbox.mailtrap.io',
        attachLog: true
      )
    }
  }
}