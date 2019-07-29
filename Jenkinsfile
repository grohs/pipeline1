pipeline {
  agent any
  stages {
    stage('Build Job Staging') {
      steps {
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
        build 'linkacopy'
      }
    }
    stage('Merge') {
      steps {
        sh '''git fetch https://github.com/grohs/pipeline1.git --all
git checkout staging
git merge $master
git checkout master
'''
      }
    }
  }
}