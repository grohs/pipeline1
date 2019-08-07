pipeline {
  agent any
  stages {
    stage('Pre Build (Staging)') {
      parallel {
        stage('Git Staging') {
          steps {
            git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
          }
        }
        stage('SonarQube') {
          steps {
            build 'capcopy'
          }
        }
      }
    }
    stage('Deploy Staging') {
      steps {
        build 'linkacopy'
      }
    }
    stage('ZAP') {
      steps {
        build 'linkacopy'
      }
    }
  }
}
