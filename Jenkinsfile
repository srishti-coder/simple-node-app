pipeline {
  agent any

  environment {
    IMAGE_NAME = 'srishti-coder/simple-node-app'
    TAG = 'latest'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/srishti-coder/simple-node-app.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$TAG .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
          sh 'docker push $IMAGE_NAME:$TAG'
        }
      }
    }
  }
}
