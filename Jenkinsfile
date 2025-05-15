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
        subject: "Build: ${env.JOB_NAME} - #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
        body: """Hi Team,

The build has completed.

🔧 Job: ${env.JOB_NAME}  
🔁 Build #: ${env.BUILD_NUMBER}  
📊 Status: ${currentBuild.currentResult}  
🔗 Details: ${env.BUILD_URL}

Regards,  
Jenkins Bot 🤖
""",
        to: 'd0fd824e61-acd2b8@inbox.mailtrap.io',  // Replace with your Mailtrap inbox
        attachLog: true
      )
    }
  }
}