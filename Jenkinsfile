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
        sh '''git checkout staging
git pull https://github.com/grohs/pipeline1.git staging
$ECHO $COMMIT_ID
git merge master $COMMIT_ID
git checkout master
'''
      }
    }
  }
}