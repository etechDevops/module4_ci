pipeline{
  agent any 
  stages{
    stage('git-clone'){
      steps{
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'test1-project', url: 'https://github.com/Abaree/module2_ci.git']]])
      }
    }
    stage('etech-hello'){
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
        sh "mvn test"
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
    stage('SonarQube - SAST') {
      steps {
        withSonarQubeEnv('SonarQube') {
          sh mvn clean verify sonar:sonar \
  -Dsonar.projectKey=3tech-demo \s.cloudapp.azure.com:0 \
  -Dsonar.login=4ac4ca52158012d7f  6d8eb
  -Dsonar.host.url=http://abaree.eastu7abdf4d25e37b5ce69900
        }
        timeout(time: 2, unit: 'MINUTES') {
          script {
            waitForQualityGate abortPipeline: true 
          }
        }
      }
    } 
  }
}
