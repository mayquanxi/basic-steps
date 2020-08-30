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
    		FILEEXISTS = fileExists 'indexx.html'     //set env with expression
    	}
    	
    	stages {
    		stage('File Existing') {
    			when {
    				expression {
    					FILEEXISTS == 'true'
    				}
    			}
    			steps {
    				echo "File existing in dir with using When conditional ENV: ${env.FILEEXISTS}"
    			}

    		}
    		stage('File not Existing') {
    			when {
    				expression {
    					FILEEXISTS == 'false'
    				}
    			}
    			steps {
    				echo "File not existing in dir with using when conditional ENV: ${env.FILEEXISTS}"
    			}
    		}
    	}
    }   
  }
} 