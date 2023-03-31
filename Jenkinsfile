pipeline {
		agent { docker { image 'maven:3.6.3'}}
		stages{
			stage('Build'){
				steps{
					sh "mvn --version"
					echo "Build"
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
