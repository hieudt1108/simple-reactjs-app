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
