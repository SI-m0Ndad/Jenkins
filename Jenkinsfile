pipeline {
  agent {
    docker {
      image 'node:18.17.1-alpine3.18'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      parallel {
        stage('Deliver') {
          steps {
            sh '''./jenkins/scripts/deliver.sh
input message: \'Finished using the web site? (Click "Proceed" to continue)\'
'''
          }
        }

        stage('Deliver-2') {
          steps {
            sh './jenkins/scripts/kill.sh'
          }
        }

      }
    }

  }
}