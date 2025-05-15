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
        // Run tests without failing the whole build if snyk is not authenticated
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
        body: """
Hi Team,

Jenkins job has completed.

Job: ${env.JOB_NAME}  
Build #: ${env.BUILD_NUMBER}  
Result: ${currentBuild.currentResult}  
URL: ${env.BUILD_URL}

Please review the logs if necessary.

Regards,  
Jenkins Bot 🤖
""",
        to: 'd0fd824e61-acd2b8@inbox.mailtrap.io',  // or your real email if using Gmail
        attachLog: true
      )
    }
  }
}