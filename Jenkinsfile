pipeline {
  agent any
  stages {
    stage('Example Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore clean package'
      }
    }
  }
}