pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'mvn -Dmaven.test.failure.ignore clean package'
      }
    }
    stage('Results') {
      steps {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
      }
   }
  }
}
