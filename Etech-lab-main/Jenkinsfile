pipeline{
	agent any 
	stages{
		stage('git-clone'){
			steps{
           checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-check', url: 'https://github.com/Etech-consulting-projects/Etech-lab']]])
			}
		}
	}	
	
}
