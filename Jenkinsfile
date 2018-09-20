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
        //Aqui estamos delegando en Maven el despliegue de la palicacion en el entorno de desarrollo
        bat 'mvn -Dmaven.test.failure.ignore clean verify -P it'
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
