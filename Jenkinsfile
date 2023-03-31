pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'}}
	//agent { docker { image 'node:13.8'}}
	environment {
		dockerHome = tool 'jkDocker'//Installed via Jenkins Global Tool Configuration
		mavenHome = tool 'jkMaven'//Installed via Jenkins Global Tool Configuration
		PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"//Adding bin folders to PATH
	}
	stages{
		stage('Build'){
			steps{
				sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Test'){
			steps{
				echo "Test"
			}
		}
		stage('IntegrationTest'){
			steps{
				echo "IntegrationTest"
			}
		}
	} 
	post {
		always {
			echo "post-stages"
		}
		success {
			echo "post-successful :)"
		}
		failure {
			echo "post-failure :("
		}
	}
}
