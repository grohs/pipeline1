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
        emailext(subject: 'Teste', body: 'Teste', to: 'support@it2sgroup.com')
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