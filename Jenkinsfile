pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat(script: '"${mvnHome}\\bin\\mvn" -Dmaven.test.failure.ignore clean package', returnStatus: true)
      }
    }
  }
}