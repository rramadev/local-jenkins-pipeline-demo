pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh scripts/deliver.sh'
      }
    }

    stage('Tests') {
      steps {
        echo 'Test demo-app'
      }
    }

    stage('Deploy Stage') {
      steps {
        echo 'Deploy to Stage'
        input 'Ok to Deploy to Prod?'
      }
    }

    stage('Deploy Prod') {
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}