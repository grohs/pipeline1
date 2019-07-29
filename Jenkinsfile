pipeline {
  agent any
  stages {
    stage('Build Job Staging') {
      steps {
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
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
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'master')
        build 'capcopy'
      }
    }
  }
}