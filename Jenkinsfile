pipeline {
  agent {
  	label 'master'
  }
  stages {
    stage('TEST') {
      steps {
      	sh 'ls -l'
        dir('dir') {
        	deleteDir()
        }
      	sh 'ls -l'
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
    stage('TEST2') {
    	steps {
    		echo message: 'this is command echo'   //full echo
    		echo "this is command echo short" //short echo
    	}
    }
    //stage('error example') {
    //	steps {
    //		error message: 'this is stage error example'   // bao co loi trong mot mot giai doan
    //	}
    //}
    stage('fileExists') {
    	environment {
    		FILEEXISTS = fileExists 'index.html'     //set env with expression
    	}
    	steps {
    		echo "${env.FILEEXISTS}"   // whill echo 'true' if file exist
    		if ( FILEEXISTS == true ) {
    			echo 'file existing on dir'
    		}
    		else {
    			echo 'file not existing on dir'
    		}
    	}
    }   
  }
} 