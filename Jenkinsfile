pipeline {
  agent { docker { 
    image 'ubuntu:latest'
    args '-u root:sudo -v withEnv(["HOME=${env.WORKSPACE}"])' 
    } }
  stages {
    stage('build') {
      steps {
        withEnv(["HOME=${env.WORKSPACE}"]) {
        sh 'apt install -y python python-pip'
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
        sh 'nohup python app.py &'  
        sh 'curl localhost:5000'
        }
      }
    }
  }
}
