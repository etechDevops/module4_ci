pipeline{
  agent any 
  tools { maven 'maven'}
  stages{

    stage('Cleanup Workspace') {
      steps {
         cleanWs()
            sh """
            echo "Hang tight, Cleaned Up Workspace For Project!!"
            """
        }
    }

    stage('git-clone'){
      steps{
         checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubpassword', url: 'https://github.com/rnfor-pro/module2_ci']]])
      }
    }
    stage('etech-hello'){
      steps{
        sh 'git version'
        sh 'mvn -v'
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
    stage('CodeQuality-SAST'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=etechspringapp \
  -Dsonar.host.url=http://etechlabs.eastus.cloudapp.azure.com:9000 \
  -Dsonar.login=01e6afa1885429be4fc842badeb6b471e94176e1'
      }
    }
    stage('Build Deploy Code') {
    when {
        branch 'dev'
    }
    steps {
        sh """
        echo "Building Artifact"
        """

        sh """
        echo "Deploying Code"
        """
    }
    }
  }    
}
