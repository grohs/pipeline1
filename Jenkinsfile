pipeline {
  agent any
  stages {
    stage('Build Job Staging') {
      steps {
        build 'linkacopy'
      }
    }
    stage('Build Check') {
      steps {
        input(message: 'Proceed to deploy at productin?', ok: 'Proceed')
      }
    }
    stage('Build Job Production') {
      steps {
        build 'capcopy'
      }
    }
  }
}