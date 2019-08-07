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
    stage('Merge and approval') {
      parallel {
        stage('Merge and approval') {
          steps {
            emailext(subject: 'Merge Approval', body: 'Do you approve?', to: 'support@it2sgroup.com', replyTo: 'support@it2sgroup.com', from: 'support@it2sgroup.com')
            input(message: 'Procced to merge and deploy at Production?', ok: 'Yes')
          }
        }
        stage('Email Notification') {
          steps {
            emailext(subject: 'abc', body: 'abc', from: 'support@its2group.com', replyTo: 'support@its2group.com', to: 'support@its2group.com')
          }
        }
        stage('Cleanup') {
          steps {
            cleanWs(cleanWhenAborted: true)
          }
        }
      }
    }
    stage('Deploy production') {
      steps {
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
        sh '''git checkout staging
git merge --no-ff --no-commit master
git reset HEAD Jenkinsfile
git checkout -- Jenkinsfile
git commit -m "merged staging into master"'''
      }
    }
    stage('Email Notification') {
      parallel {
        stage('Email Notification') {
          steps {
            emailext(subject: 'abc', body: 'abc', to: 'support@it2sgroup.com', replyTo: 'support@it2sgroup.com', from: 'support@it2sgroup.com')
          }
        }
        stage('Cleanup') {
          steps {
            cleanWs()
          }
        }
      }
    }
  }
}