pipeline {
  agent any
  stages {
    stage('Git staging') {
      steps {
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
      }
    }
    stage('Merge') {
      steps {
        sh '''git fetch --all
git checkout staging
git merge $master --no-commit
git checkout master
'''
      }
    }
  }
}