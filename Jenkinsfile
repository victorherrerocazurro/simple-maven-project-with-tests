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
        branch 'develop' 
      }
      steps {
        //Aqui estamos delegando en Maven el despliegue de la palicacion en el entorno de desarrollo
        bat 'mvn -Dmaven.test.failure.ignore clean verify -P it'
      }
    }
    stage('QA/Performance') {
      when { 
        branch 'release/*' 
      }
      parallel {
        stage('QA') {
          stages {
            stage('Despliegue'){
              agent 'qa'
              steps {
                //Desplegar en el entorno de QA. dos formas
                //- Con maven
                //bat 'mvn <plugin de maven que realiza el despliegue>:<goal que realiza el despliegue>'
                //- Con agentes de Jenkins
              }
            }
            stage('Verificacion'){
              input {
                message "Se ha cubierto el plan de pruebas?"
                ok "Si"
                submitter "qa"
                parameters {
                  string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
              }
            }
          }
        }
        stage('Performance') {
          steps {
            //Desplegar Servidor de Preproduccion que generalmente estará arrancado, sobre el que desplegamos
            //- Hacerlo con maven
            //Lanzar los test
            bat 'mvn -Dmaven.test.failure.ignore clean verify -P pt'
          }
        }
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
