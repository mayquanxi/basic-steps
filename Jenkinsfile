pipeline {
  agent {
  	label 'master'
  }
  stages {
    stage('TEST') {
      steps {
        dir('dir') {
        	deleteDir()
        }
      }   
      post {
        success { 
        	echo 'Post success will still run' 
        }
        failure { 
        	echo 'I will not run!' 
        }
      }   
    }   
  }
} 