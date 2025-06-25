pipeline {
  agent any

  stages {
    stage('Install dependencies') {
      agent {
        docker {
          image 'node:18'
        }
      }
      steps {
        sh 'npm install'
      }
    }

    stage('Build React App') {
      agent {
        docker {
          image 'node:18'
        }
      }
      steps {
        sh 'npm run build'
      }
    }

    stage('Archive build output') {
      steps {
        archiveArtifacts artifacts: 'build/**', fingerprint: true
      }
    }

    stage('Serve React via Docker') {
      steps {
        sh '''
          docker rm -f react-viewer || true
          docker run -d -p 3000:80 \
            -v $WORKSPACE/build:/usr/share/nginx/html \
            --name react-viewer nginx
        '''
      }
    }
  }
}
