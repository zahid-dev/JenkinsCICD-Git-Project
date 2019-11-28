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
	post {
		        success {
            emailext (
                to: "zahid.shakeel@outlook.com; zahid.shakeel@emumba.com",
                subject: "SUCCESS",
                body: "SUCCESS!"
            )
        }
        failure {
			emailext (
                to: "zahiddev.shakeel@gmail.com",
                subject: "FAILURE",
                body: "FAILURE!"
            )
        }
	}
}
