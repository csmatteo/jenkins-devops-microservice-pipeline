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
		stage('Checkout'){
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
		stage('Compile'){
			steps{
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps{
				sh "mvn test"
			}
		}
		stage('IntegrationTest'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"//failsafe plugin is included
			}
		}

		stage('Package'){
			steps{
				sh "mvn package -DskipTests"//creates JAR used to create docker image
			}
		}

		stage('Build Docker Image'){
			steps {
				//docker build -t matteodce/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("matteodce/currency-exchange-devops:${env.BUILD_TAG}")//same, but done with a script
				}
			}
		}

		stage('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('', 'dockerhub'){//first field empty because default is dockerhub, second field is credentials ID
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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
