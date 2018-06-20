pipeline {
  agent any
  stages {
    stage('Example Build') {
      steps {
        bat 'mvn -Dmaven.test.failure.ignore clean package'
      }
    }
  }
}