pipeline{
  agent any 
  stages{
    stage('git-clone'){
      steps{
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'test1-project', url: 'https://github.com/Abaree/module2_ci']]])
      }
    }
    stage('etech-hello'){
      steps{
        sh 'git version'
        sh 'java --version'
      }
    }
  }
}
