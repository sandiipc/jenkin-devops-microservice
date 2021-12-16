//SCRIPTED
/*
node {

	echo "Build"	
	echo "Test"	
	echo "Integration Test"
	
}
*/

//DECLARATIVE
pipeline {
	agent any
	//agent {docker {image 'maven:3.6.3'} }
	//agent {docker {image 'node:latest'} }
	stages {
		stage ('Build') {
			steps {
				//sh "chmod +x -R ${env.WORKSPACE}"
				//sh "./shcmd.sh"
				//sh "node --version"
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "$env.BUILD_ID"
				echo "$env.JOB_NAME"
				echo "$env.BUILD_TAG"
			}
		}
		stage ('Test') {
			steps {
				echo "Test"
			}
		}
		stage ('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} 
	post {
		always {
			echo 'I run always'
		}
		success {
			echo 'I run when build succeeded'
		}
		failure {
			echo 'I run when build failed'
		}

	}
	
}