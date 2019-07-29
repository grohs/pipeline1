pipeline {
  agent any
  stages {
    stage('Git Staging') {
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
      steps {
        emailext(subject: 'Merge Approval', body: 'Do you approve?', to: 'support@it2sgroup.com', replyTo: 'support@it2sgroup.com', from: 'support@it2sgroup.com')
        input(message: 'Procced to merge and deploy at Production?', ok: 'Yes')
      }
    }
    stage('Deploy production') {
      steps {
        build 'capcopy'
      }
    }
    stage('Email + Cleanup') {
      steps {
        emailext(subject: 'abc', body: 'abc', to: 'support@it2sgroup.com', replyTo: 'support@it2sgroup.com', from: 'support@it2sgroup.com')
        cleanWs(cleanWhenSuccess: true, skipWhenFailed: true)
      }
    }
  }
}