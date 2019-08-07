pipeline {
  agent any #This means that the script will run on your CI machine, and will use its environment as is.
  stages {
    stage('Build') { #Each stage gets a graphical representation on the blue ocean UI
      steps {
        script{
			#Putting here all the steps necessary to realize a local build
            echo "Starting Build, triggered by $BRANCH_NAME";
            echo "Building ${env.BUILD_ID}";
            sh 'composer install';
            sh 'npm install';
            sh 'node_modules/bower/bin/bower install'
            sh 'node_modules/gulp/bin/gulp.js build'
        }
      }
    }
    stage('Test') {
      steps {
        echo 'Starting Unit Tests'
        sh 'phpunit';
      }
    }
    stage('deploy develop branch') {
        when { branch 'develop' } #condition on branch name
        steps {
            script {
                echo "Deploying Develop Branch"
                def creds = loadCreds('preprod_credentials'); #This is a credential secret file loaded here
                deployCode(creds); #send code to remote environment
                deployDbChanges(creds); #send db changes instructions
                execDbChanges(creds,'preprod'); #execute db changes on remote machine
            }
        }
    }
    stage('deploy master branch') {
        when { branch 'master' } #same here for master branch
        steps {
            script {
                echo "Deploying Master Branch"
                def creds = loadCreds('prod_credentials');
                deployCode(creds);
                deployDbChanges(creds);
                execDbChanges(creds,'prod');
            }
        }
    }
    stage('notify'){ #when all is done, send a slack notification
        steps {
            script {
                slackSend(message: getChangeString(), channel: '#jenkins', color: 'good', failOnError: true, teamDomain: 'yourteam', token: 'yourtoken')
            }
        }
    }
  }
}
