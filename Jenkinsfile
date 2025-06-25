pipeline {
  agent {
    docker {
      image 'node:18'
    }
  }
  stages {
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build React App') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Archive build output') {
      steps {
        archiveArtifacts artifacts: 'build/**', fingerprint: true
      }
    }
  }
}
