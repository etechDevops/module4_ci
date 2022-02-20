pipeline{
	agent any 
	stages{
		stage('git-clone'){
			steps{
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-checkid', url: 'https://github.com/etechDevops/module2_ci']]])
			}
		}
		stage('etech-hello'){
			steps{
				sh 'git version'
				sh 'mvn -v'
				// comments //
			       
			}
		}
	}	
	
}
