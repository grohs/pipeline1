pipeline {
  agent any
  stages {
    stage('Pre Build (Staging)') {
      parallel {
        stage('Git Staging') {
          steps {
            git(url: 'https://github.com/grohs/pipeline1.git', branch: 'mixed')
          }
        }
        stage('SonarQube') {
          steps {
            sh '/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner -Dsonar.host.url=http://192.168.0.14:9000 -Dsonar.projectName=pipeline1_mixed -Dsonar.projectVersion=1.0 -Dsonar.projectKey=pipeline1_mixed.com.br -Dsonar.sources=. -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/pipeline1_mixed'
          }
        }
      }
    }
    stage('Deploy Staging') {
      steps {
        sh '/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner -Dsonar.host.url=http://192.168.0.14:9000 -Dsonar.projectName=pipeline1_mixed -Dsonar.projectVersion=1.0 -Dsonar.projectKey=pipeline1_mixed.com.br -Dsonar.sources=. -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/pipeline1_mixed'
      }
    }
    stage('ZAP') {
      steps {
        sh '/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner -Dsonar.host.url=http://192.168.0.14:9000 -Dsonar.projectName=pipeline1_mixed -Dsonar.projectVersion=1.0 -Dsonar.projectKey=pipeline1_mixed.com.br -Dsonar.sources=. -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/pipeline1_mixed'
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
        git(url: 'https://github.com/grohs/pipeline1.git', branch: 'master')
        sh '''git config --global merge.ours.driver true
git checkout staging
git pull origin staging
git merge --no-ff --no-commit master
git reset HEAD Jenkinsfile
git checkout -- Jenkinsfile
git commit -m "merged staging into master"
git push origin staging'''
      }
    }
    stage('Email Notification') {
      steps {
        emailext(subject: 'abc', body: 'abc', to: 'support@it2sgroup.com', replyTo: 'support@it2sgroup.com', from: 'support@it2sgroup.com')
      }
    }
  }
}