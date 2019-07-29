pipeline {
  agent any
  stages {
    stage('Build Job Staging') {
      parallel {
        stage('Build Job Staging') {
          steps {
            build 'linkacopy'
          }
        }
        stage('git staging') {
          steps {
            git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
          }
        }
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