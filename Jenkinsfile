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
            withSonarQubeEnv 'SonarQube'
          }
        }
        stage('') {
          steps {
            waitForQualityGate true
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
      }
    }
    stage('Deploy production') {
      steps {
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'staging')
        sh '''git pull origin staging
git merge master
git reset HEAD Jenkinsfile
git checkout -- Jenkinsfile
git push origin staging
'''
      }
    }
    stage('Email Notification') {
      steps {
        emailext(subject: 'abc', body: 'abc', to: 'support@it2sgroup.com', replyTo: 'support@it2sgroup.com', from: 'support@it2sgroup.com')
      }
    }
  }
}