pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t app .'
      }
    }
    stage('Test') {
      steps {
        echo 'Test'
        sh '/bin/nc -vz localhost 22'
        sh '/bin/nc -vz localhost 80'
      }
    }
    stage('Push Registry') {
      steps {
        echo 'Push to Docker registry'
        sh 'docker tag ap:test app:stable'
        sh 'docker push app:test app:stable'
      }
    }
  }
}
