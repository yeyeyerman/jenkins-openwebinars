pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build'
        sh 'docker build -t app:test .'
      }
    }
    stage('Test') {
      steps {
        echo 'Test'
        sh 'docker run -p 80:80 -d --name app-container --rm app:test'
        sh '/bin/nc -vz localhost 80'
      }
      post {
        always {
          sh 'docker container stop app-container'
        }
      }
    }
    stage('Push to registry') {
      steps {
        echo 'Push to Docker registry'
        withDockerRegistry([credentialsId: 'DockerHub', url: '']) {
          sh 'docker tag app:test gpsantosb/app:stable'
          sh 'docker push gpsantosb/app:stable'
        }  
      }
    }
  }
}
