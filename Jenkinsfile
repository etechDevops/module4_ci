pipeline{
  agent any 
  stages{
    stage('git-clone'){
      steps{
          git changelog: false, credentialsId: 'test1-project', poll: false, url: 'https://github.com/Abaree/module2_ci'
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
