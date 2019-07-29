pipeline {
  agent any
  stages {
    stage('Build Job Staging') {
<<<<<<< HEAD
      steps {
        build 'linkacopy'
=======
      steps {
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'master')
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
>>>>>>> b6e46c3cad204dda211427fb17168ef7d7b483a2
      }
    }
  }
}