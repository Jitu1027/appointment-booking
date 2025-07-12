pipeline {
  agent any

  environment {
    DOCKER_IMAGE = 'medibook-app'
    CONTAINER_NAME = 'medibook-container'
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/Jitu1027/appointment-booking.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Build App') {
      steps {
        bat 'npm run build'
      }
    }

    stage('Docker Build') {
      steps {
        bat 'docker build -t %DOCKER_IMAGE% .'
      }
    }

    stage('Docker Run') {
      steps {
        bat '''
          docker stop %CONTAINER_NAME% || exit 0
          docker rm %CONTAINER_NAME% || exit 0
          docker run -d -p 3000:3000 --name %CONTAINER_NAME% %DOCKER_IMAGE%
        '''
      }
    }
  }
}
