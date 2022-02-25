pipeline{
   agent any
   tools {maven 'maven'}
   stages{
    stage('git-clone'){
            steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-check', url: 'https://github.com/dilanAzu/module2_ci']]])
         }
       }
      stage('dilanAzu-hello'){
         steps{
            sh 'git version' 
          }
      }
     stage('Build Artifact - Maven') {
        steps {
        sh "mvn clean package -DskipTests=true"
        archive 'target/*.jar'
      }
    }
    stage('Unit Tests - JUnit and JaCoCo') {
      steps {
        sh 'mvn test'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
    }
    stage('Mutation Tests - PIT') {
      steps {
        sh "mvn org.pitest:pitest-maven:mutationCoverage"
      }
      post {
        always {
          pitmutation mutationStatsFile: '**/target/pit-reports/**/mutations.xml'
        }
      }
    }
      stage('Code Quality-SAAT'){
         steps{
         sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=devsecops-spring-app \
  -Dsonar.host.url=http://dilandemo.eastus.cloudapp.azure.com:9000 \
  -Dsonar.login=3f51c15d8beee129167eb2344243e7e3bbcbca83' 
      }  
    }
  }
}
