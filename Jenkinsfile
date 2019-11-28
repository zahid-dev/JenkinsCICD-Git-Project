pipeline {
  agent { docker { image 'python:3.7.4' } }
  stages {
    stage('build') {
      steps {
        withEnv(["HOME=${env.WORKSPACE}"]) {
        sh 'pip install --user -r requirements.txt'
        }
      }
    }
    stage('unittest') {
      steps {
        withEnv(["HOME=${env.WORKSPACE}"]) {
        sh 'python test.py'
        }
      }
      post {
        always {
          withEnv(["HOME=${env.WORKSPACE}"]) {
          junit 'test-reports/*.xml'
          }
        } 
      }  
    }
    stage('functionaltest') {
      when {
        expression { return params.current_status == "closed" && params.merged == true }
      }
      steps {
        withEnv(["HOME=${env.WORKSPACE}"]) {
        sh 'curl localhost:5000'
        }
      }
    }
  }
}
