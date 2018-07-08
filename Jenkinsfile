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
        docker run -p 80:80 -id --name app --rm app
        sh '/bin/nc -vz localhost 80'
      }
      post {
        always {
          sh 'docker container stop app'
        }
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
