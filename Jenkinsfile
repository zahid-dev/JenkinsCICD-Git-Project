pipeline {
  agent { docker { image 'python:3.7.4' } }
  stages {
    stage('build') {
      /*when {
                  sh 'echo $params.current_status'
                  expression { return params.current_status == "closed" && params.merged == true }
              }*/
      steps {
        withEnv(["HOME=${env.WORKSPACE}"]) {
          sh "echo ${params.ccurrent_status}"
          sh "echo ${params.merged}"
        sh 'pip install --user -r requirements.txt'
        }
      }
    }
    stage('test') {
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
  }
}
