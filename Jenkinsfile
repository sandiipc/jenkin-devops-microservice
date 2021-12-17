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
	environment {
		dockerHome = tool 'jenkinsDocker'
		mavenHome = tool 'jenkinsMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage ('Checkout') {
			steps {
				//sh "chmod +x -R ${env.WORKSPACE}"
				//sh "./shcmd.sh"
				//sh "node --version"
				//sh "docker version"
				sh "mvn --version"				
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
			}
		}
		stage ('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage ('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage ('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage ('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		
		stage ('Build Docker Image') {
			steps {
				script {
					dockerImage = docker.build("sandiipc/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage ('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
					
				}
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