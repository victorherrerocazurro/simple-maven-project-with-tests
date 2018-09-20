pipeline {
  agent any
  stages {
    stage('UT') {
      when {
        branch 'feature/*'
      }
      steps {
        bat 'mvn -Dmaven.test.failure.ignore clean verify -P ut'
      }
    }
    stage('IT') {
      when {
        branch 'master'
      }
      steps {
        bat 'mvn -Dmaven.test.failure.ignore clean verify -P it'
      }
    }
    stage('QA/Performance') {
      parallel {
        stage('QA') {
          steps {
            bat 'mvn'
            input(message: 'Finalizaron correctamente', submitter: 'qa')
          }
        }
        stage('Performance') {
          steps {
            bat 'mvn'
          }
        }
      }
    }
  }
}