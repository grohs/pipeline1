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
$ECHO $COMMIT_ID
git checkout master
'''
      }
    }
  }
}