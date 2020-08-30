pipeline {
  agent {
  	label 'master'
  }
  options { skipDefaultCheckout() }
  stages {
    stage('catchError') {
      steps {
        catchError {
          error 'Force error'
        }
        echo 'This echo still runs'
      }   
      post {
        success { echo 'Post success will still run' }
        failure { echo 'I will not run!' }
      }   
    }   
  }
} 