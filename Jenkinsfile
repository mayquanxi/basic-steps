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
    stage('echo, pwd and readFile') {
    	options {
    		retry count: 2                        //retry happen when error inside or co ngoai le nao gay ra khien duong ong khong thanh cong.
    		timeout(time: 5, unit: MINUTES)
    	}
    	environment	{
    		PWD = pwd()
    		READFILE = readFile file: "./dir2/newfile"
    	}
    	steps {
    		echo message: 'this is command echo'   //full echo
    		echo "this is command echo short" //short echo
    		echo "ENV: ${env.PWD}"    				//echo PWD
    		retry(2){								//retry say ra khi lenh ben trong say ra loi khong cho ket qua nhu mong doi
    			echo "ENV: ${env.READFILE}" // echo readfile newfile
    		}
    	}
    }
    //stage('error example') {
    //	steps {
    //		error message: 'this is stage error example'   // bao cao co loi tren mot giai doan 
    //	}
    //}
    stage('fileExists') {
    	environment {
    		FILEEXISTS = fileExists 'index.html'     //set env with expression
    	}
    	//steps {
    	//    echo "${env.FILEEXISTS}"   // whill echo 'true' if file exist
    	//    echo "current branch: ${env.BRANCH_NAME}"
    	//    script {											//khai bao script for if else
    	//    	if (env.FILEEXISTS == 'true') {
    	//    		echo 'file existing on dir'
    	//        }
    	//    	else {
    	//    		echo 'file not existing on dir'
    	//    	}
    	//    }
    	//}
    	stages {							//co giai doan nay thi khong co steps phia ben tren
    		stage('File Existing') {   							//use fileExists for when conditional
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
    stage('isUnix') {
    	environment { 
    		ISUNIX = isUnix()
    	}
    	steps {
    		script {
    			if (env.ISUNIX == 'true') {
    				echo "pipeline currently on linux or OSX ENV: ${env.ISUNIX}"
    			}
    			else {
    				echo "pipeline currently on Windows: ${env.ISUNIX}"
    			}
    		}
    	}
    }
    stage('MAIL') {
    	environment {
    		MYNAME = "NGUYEN KHAC MANH"
    	}
    	steps {
    		mail (
    			subject: "TEST MAIL",
    			body: "THIS IS TEST MAIL ENV: ${env.MYNAME}",
    			to: "khacmanhk45s1@gmail.com",
    			from: "mayquanxi@gmail.com",
    			cc: "mayquanxi@gmail.com"
    		)
    	}
    }

  }
} 