pipeline{
	agent any
	tools {maven 'maven'}
	stages{
    stage('git-clone'){
            steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-check', url: 'https://github.com/dilanAzu/module2_ci']]])
         }
       }
      stage('etech-hello'){
	steps{
          sh 'git version'
	  sh 'mvn' -v	
       }
     }
     stage('Build Artifacts - maven'){
	steps {
	  sh "mvn package -Dkiptest-true"
	  archive 'target/*.jar'
	}
      } 
    }

 }
		
     
  
